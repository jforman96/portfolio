# Security Headers Setup for www.jflab.cz

## Problem
GitHub Pages doesn't support custom HTTP security headers natively. Meta tags provide limited coverage, but HTTP headers require middleware.

## Solution: Cloudflare Workers

To add HTTP security headers to www.jflab.cz hosted on GitHub Pages:

### Prerequisites
- Cloudflare account (free tier works)
- www.jflab.cz domain DNS managed by Cloudflare

### Setup Steps

1. **Point DNS to Cloudflare** (if not already done)
   - Update your domain registrar to use Cloudflare nameservers
   - Create a CNAME record: `www.jflab.cz CNAME jforman96.github.io`

2. **Create Cloudflare Worker**
   - Go to [Cloudflare Dashboard](https://dash.cloudflare.com/) → Workers
   - Create a new Worker named `jflab-security-headers`
   - Paste the following code:

```javascript
export default {
  async fetch(request) {
    const response = await fetch(request);
    const newResponse = new Response(response.body, response);
    
    // Add security headers
    newResponse.headers.set('Strict-Transport-Security', 'max-age=31536000; includeSubDomains; preload');
    newResponse.headers.set('X-Content-Type-Options', 'nosniff');
    newResponse.headers.set('X-Frame-Options', 'DENY');
    newResponse.headers.set('X-XSS-Protection', '1; mode=block');
    newResponse.headers.set('Referrer-Policy', 'strict-origin-when-cross-origin');
    newResponse.headers.set('Permissions-Policy', 'geolocation=(), microphone=(), camera=(), payment=()');
    newResponse.headers.set('Content-Security-Policy', "default-src 'self'; script-src 'self' https://cdnjs.cloudflare.com https://cdn.jsdelivr.net; style-src 'self' 'unsafe-inline' https:; font-src 'self' https:; img-src 'self' https: data:; frame-ancestors 'none'; object-src 'none'; base-uri 'self';");
    
    return newResponse;
  },
};
```

3. **Deploy Worker**
   - Click "Save and Deploy"

4. **Add Route**
   - In Worker settings, add a route: `www.jflab.cz/*`
   - Bind the route to `jflab-security-headers` worker

5. **Verify**
   - Test with: `curl -I https://www.jflab.cz | grep -i x-frame`
   - Check [securityheaders.com](https://securityheaders.com/?q=www.jflab.cz)

## Expected Result
After setup, you should see:
- ✅ A+ or A rating on securityheaders.com
- ✅ All security headers present in HTTP responses

## References
- [Cloudflare Workers Docs](https://developers.cloudflare.com/workers/)
- [Security Headers Guide](https://securityheaders.com)
