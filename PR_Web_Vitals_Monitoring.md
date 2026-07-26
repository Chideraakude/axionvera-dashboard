# Web Vitals Performance Monitoring

## Summary

Enabled Web Vitals monitoring to track real-world performance metrics (LCP, FID, CLS) across different geographic locations. This helps identify performance issues that affect real users in production.

## Problem Solved

The team needed to know if the dashboard is slow for real-world users in different geographic locations. Without Web Vitals monitoring, there was no visibility into Core Web Vitals metrics that impact user experience and SEO.

## Solution Overview

Imported and integrated the `reportWebVitals` function from the `web-vitals` package in `_app.tsx` to collect performance metrics on every page load.

### Files Modified

| File | Changes |
|------|---------|
| `src/pages/_app.tsx` | Added `reportWebVitals` import and integration |

## Technical Details

- **Package Used**: `web-vitals@^5.2.0` (already installed as dependency)
- **Metrics Monitored**:
  - **LCP** (Largest Contentful Paint) - measures loading performance
  - **FID** (First Input Delay) - measures interactivity
  - **CLS** (Cumulative Layout Shift) - measures visual stability
  - **TTFB** (Time to First Byte) - measures server responsiveness
  - **FCP** (First Contentful Paint) - measures perceived load speed
  - **INP** (Interaction to Next Paint) - measures responsiveness

## Implementation Details

```typescript
// Import reportWebVitals
import { reportWebVitals } from 'web-vitals';

// Callback function to handle metrics
function onWebVitals(metric: any) {
  console.debug('Web Vitals metric:', metric.name, metric.value);
  // Optionally send to analytics service (GA4, etc.)
}

// Integrate in useEffect
useEffect(() => {
  reportWebVitals(onWebVitals);
}, []);
```

## Acceptance Criteria

- [x] Import `reportWebVitals` function in `_app.tsx`
- [x] Use `reportWebVitals` to monitor LCP (Largest Contentful Paint)
- [x] Use `reportWebVitals` to monitor FID (First Input Delay)
- [x] Use `reportWebVitals` to monitor CLS (Cumulative Layout Shift)
- [x] Web Vitals package already available in dependencies

## Vercel Integration (Zero Config)

When deployed to Vercel, this is a "Zero Config" feature:
1. Go to **Project Settings** → **Analytics** in Vercel dashboard
2. Enable "Web Vitals" monitoring
3. Metrics will automatically appear in the Vercel Analytics dashboard

## Testing Steps

### Step 1: Verify Code Changes
```bash
git diff src/pages/_app.tsx
```
Expected: Shows new `reportWebVitals` import and `onWebVitals` callback

### Step 2: Run Development Server
```bash
npm run dev
```

### Step 3: Test in Browser
1. Navigate to `http://localhost:3000`
2. Open browser **Console** tab in DevTools
3. Refresh the page
4. Verify console shows Web Vitals metrics:
   ```
   Web Vitals metric: LCP <value>
   Web Vitals metric: FID <value>
   Web Vitals metric: CLS <value>
   ```

### Step 4: Deploy to Vercel (Production)
1. Deploy the branch to Vercel
2. Go to Vercel Dashboard → Project → Analytics
3. Enable Web Vitals if not already enabled
4. Wait for real user metrics to populate

## Related Documentation

- [web-vitals library](https://www.npmjs.com/package/web-vitals)
- [Vercel Web Vitals Analytics](https://vercel.com/docs/concepts/analytics/web-vitals)