# Cookie Consent Banner — Implementation Guide

This guide covers implementing a GDPR-compliant cookie consent banner in a React application.

## How it works

1. On first visit, check for the `gdpr_consent` cookie
2. If absent, show the consent banner — block all non-essential scripts until the user decides
3. If present, read the value and conditionally load scripts accordingly

## Cookie Consent Cookie

Store the user's choice in a first-party cookie:
```
gdpr_consent=accepted    (user clicked "Accept All")
gdpr_consent=rejected    (user clicked "Reject Non-Essential")
```

Expiry: 12 months from consent date.

---

## React Component — `ConsentBanner.tsx`

```tsx
import { useEffect, useState } from 'react';

type ConsentStatus = 'accepted' | 'rejected' | null;

function getCookie(name: string): string | null {
  const match = document.cookie.match(new RegExp('(^| )' + name + '=([^;]+)'));
  return match ? match[2] : null;
}

function setCookie(name: string, value: string, days: number) {
  const expires = new Date(Date.now() + days * 864e5).toUTCString();
  document.cookie = `${name}=${value}; expires=${expires}; path=/; SameSite=Lax`;
}

export function ConsentBanner() {
  const [status, setStatus] = useState<ConsentStatus>(null);
  const [visible, setVisible] = useState(false);

  useEffect(() => {
    const existing = getCookie('gdpr_consent') as ConsentStatus;
    if (existing) {
      setStatus(existing);
      applyConsent(existing);
    } else {
      setVisible(true); // Show banner
    }
  }, []);

  function applyConsent(choice: 'accepted' | 'rejected') {
    if (choice === 'accepted') {
      // Load your tracking script here
      loadTrackerScript();
    }
    // If rejected, do nothing — tracker never loads
  }

  function handleAccept() {
    setCookie('gdpr_consent', 'accepted', 365);
    setStatus('accepted');
    setVisible(false);
    applyConsent('accepted');
  }

  function handleReject() {
    setCookie('gdpr_consent', 'rejected', 365);
    setStatus('rejected');
    setVisible(false);
  }

  if (!visible) return null;

  return (
    <div style={{
      position: 'fixed', bottom: 0, left: 0, right: 0,
      background: '#1a1a2e', color: '#fff', padding: '1.5rem',
      zIndex: 9999, display: 'flex', flexWrap: 'wrap',
      alignItems: 'center', justifyContent: 'space-between', gap: '1rem'
    }}>
      <p style={{ margin: 0, maxWidth: '600px', fontSize: '0.9rem' }}>
        🍪 We use cookies and analytics to improve your experience.
        By clicking "Accept All", you consent to our use of tracking technologies.
        Read our <a href="/privacy" style={{ color: '#a0c4ff' }}>Privacy & Cookie Policy</a>.
      </p>
      <div style={{ display: 'flex', gap: '0.75rem' }}>
        <button
          onClick={handleReject}
          style={{ padding: '0.5rem 1rem', background: 'transparent',
            border: '1px solid #aaa', color: '#aaa', borderRadius: '6px', cursor: 'pointer' }}
        >
          Reject Non-Essential
        </button>
        <button
          onClick={handleAccept}
          style={{ padding: '0.5rem 1rem', background: '#4f46e5',
            border: 'none', color: '#fff', borderRadius: '6px', cursor: 'pointer' }}
        >
          Accept All
        </button>
      </div>
    </div>
  );
}
```

---

## Loading the Tracker Script Conditionally

Replace any hard-coded `<script>` tag in the HTML with a JavaScript-controlled loader:

```typescript
// src/utils/tracker.ts
export function loadTrackerScript() {
  const trackingId = import.meta.env.VITE_TRACKING_ID; // Set your tracking ID in env
  if (!trackingId) return;

  const existing = document.getElementById('ci-tracker');
  if (existing) return; // Don't load twice

  const script = document.createElement('script');
  script.id = 'ci-tracker';
  script.src = `${import.meta.env.VITE_APP_URL || ''}/tracker.js`;
  script.setAttribute('data-tracking-id', trackingId);
  document.head.appendChild(script);
}
```

---

## Mounting the Banner

Add `<ConsentBanner />` at the root of your app, inside `App.tsx`:

```tsx
import { ConsentBanner } from './components/ConsentBanner';

function App() {
  return (
    <>
      <ConsentBanner />
      {/* ... rest of app ... */}
    </>
  );
}
```

---

## Optional: Consent Management Link in Footer

Let users revisit their choice by resetting the cookie:

```tsx
function ManageConsent() {
  function reset() {
    document.cookie = 'gdpr_consent=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;';
    window.location.reload();
  }
  return (
    <button onClick={reset} style={{ background: 'none', border: 'none',
        textDecoration: 'underline', cursor: 'pointer', color: 'inherit' }}>
      Manage Cookie Preferences
    </button>
  );
}
```
