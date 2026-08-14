# Troubleshooting & Maintenance Guide

## 🔧 Common Issues & Solutions

### 1. SVG Images Not Displaying

#### Symptom
SVGs show as broken images or don't render

#### Causes & Solutions

| Cause | Solution |
|-------|----------|
| Incorrect file path | Check relative paths (./assets/filename.svg) |
| SVG syntax error | Validate SVG with [SVG Validator](https://www.w3.org/Icons/svg-edit/) |
| MIME type incorrect | Server should serve SVG as `image/svg+xml` |
| Browser cache | Clear browser cache (Ctrl+Shift+Delete) |
| GitHub rendering | Use raw.githubusercontent.com for correct MIME type |

#### Quick Fix
```bash
# Validate SVG syntax
xmllint --noout assets/profile-hero.svg

# Check file exists
ls -lh assets/profile-*.svg
```

### 2. Animations Not Playing

#### Symptom
SVG animations don't animate, or animations are jumpy

#### Causes & Solutions

| Cause | Solution |
|-------|----------|
| prefers-reduced-motion enabled | User has motion reduction enabled (intentional) |
| Browser doesn't support SVG animations | Use static fallback |
| Animation syntax error | Check @keyframes definition |
| Animation duration too short | Increase from 200ms to minimum 400ms |
| Frame rate issues | Check browser DevTools → Performance |

#### Quick Diagnostics
```javascript
// Check if animations supported
const hasAnimationSupport = CSS.supports('animation-name', 'test');
console.log('Animation support:', hasAnimationSupport);

// Check prefers-reduced-motion
const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
console.log('Reduced motion preferred:', prefersReduced);
```

### 3. External Service Badges Not Loading

#### Symptom
GitHub stats badges show broken images

#### Causes & Solutions

| Cause | Solution |
|-------|----------|
| Service temporarily down | Use fallback SVG (automatic) |
| Network timeout | Browser switches to fallback after 3s |
| Rate limiting | GitHub badges cache after first request |
| Old cache | Force refresh (Ctrl+Shift+R or Cmd+Shift+R) |

#### Verify Fallback Works
```bash
# Test fallback SVG exists
ls -la assets/stats-fallback-*.svg

# If fallback missing, regenerate:
# See assets/ directory for SVG files
```

### 4. Mobile Layout Broken

#### Symptom
Content doesn't fit on mobile or overlaps

#### Causes & Solutions

| Cause | Solution |
|-------|----------|
| Missing viewport meta | Add `<meta name="viewport">` |
| Fixed widths | Use percentages or max-width |
| Horizontal overflow | Remove overflow-x or use flex-wrap |
| SVG not responsive | Add `width="100%"` to SVG elements |
| Tables too wide | Use horizontal scroll or stack on mobile |

#### Mobile Testing Checklist
```html
<!-- Correct viewport setting -->
<meta name="viewport" content="width=device-width, initial-scale=1">

<!-- Responsive image -->
<img src="image.svg" alt="..." style="width: 100%; max-width: 1200px;">

<!-- Responsive table -->
<div style="overflow-x: auto;">
  <table>...</table>
</div>
```

### 5. Links Not Working

#### Symptom
Clicked links don't navigate or show errors

#### Causes & Solutions

| Cause | Solution |
|-------|----------|
| Incorrect URL | Verify link URL in QUALITY_ASSURANCE.md |
| User account changed | Update username in all links |
| Profile made private | Repository must be public |
| Mailto link issues | Check email format (montanajeremy160@outlook.com) |
| GitHub account issues | Verify @HomieB-tt still exists |

#### Link Validation Command
```bash
# Check for broken links (requires linkchecker)
brew install linkchecker  # or apt-get install linkchecker
linkchecker README.md
```

### 6. Performance Issues

#### Symptom
Profile loads slowly or animations are choppy

#### Causes & Solutions

| Cause | Solution |
|-------|----------|
| Large SVG files | Optimize using SVGO (see PERFORMANCE.md) |
| Too many animations | Reduce simultaneous animations |
| External service slow | Use fallback, check service status |
| Network throttling | Check DevTools Network tab |
| Old device/browser | Update browser or use static fallbacks |

#### Performance Debugging
```javascript
// Measure load time
console.time('profile-load');
// ... measure something ...
console.timeEnd('profile-load');

// Check animation frame rate
let lastTime = performance.now();
function checkFPS() {
  const now = performance.now();
  const fps = 1000 / (now - lastTime);
  console.log('FPS:', fps);
  lastTime = now;
  requestAnimationFrame(checkFPS);
}
```

## 🛠️ Maintenance Tasks

### Daily Tasks (Automated)
- Monitor external service status
- Track broken links
- Monitor performance metrics

### Weekly Tasks
- [ ] Review stats accuracy
- [ ] Check link functionality
- [ ] Verify animations smooth
- [ ] Monitor user feedback
- [ ] Check for browser issues

### Monthly Tasks
- [ ] Run Lighthouse audit
- [ ] Review and update tech stack if needed
- [ ] Verify all external services working
- [ ] Check analytics/engagement
- [ ] Update learning progress if changed
- [ ] Review project status updates
- [ ] Test on new browser versions
- [ ] Check mobile rendering

### Quarterly Tasks
- [ ] Major design review
- [ ] Update DESIGN_SYSTEM.md
- [ ] Review performance trends
- [ ] Plan next improvements
- [ ] Update project descriptions
- [ ] Archive old projects
- [ ] Security audit

### Annual Tasks
- [ ] Complete rebranding if needed
- [ ] Rebuild from scratch if major changes
- [ ] Update year in copyright
- [ ] Long-term performance analysis
- [ ] Strategic review of brand identity

## 📋 Update Checklist

When updating the profile, follow this checklist:

### Before Making Changes
- [ ] Create backup of current README.md
- [ ] Note current performance metrics
- [ ] Document what will change
- [ ] Plan rollback strategy

### Making Changes
- [ ] Update appropriate file (README.md, SVG, etc.)
- [ ] Verify syntax (no broken markdown/SVG)
- [ ] Test locally if possible
- [ ] Check all links still work
- [ ] Verify animations (if changed)

### Testing Changes
- [ ] View on desktop browser
- [ ] Test on mobile device
- [ ] Check accessibility (screen reader, keyboard)
- [ ] Verify animations smooth
- [ ] Confirm external services load
- [ ] Test with animations disabled
- [ ] Check performance impact

### After Deployment
- [ ] Clear browser cache
- [ ] Verify live version displays correctly
- [ ] Test all links from live version
- [ ] Monitor for issues
- [ ] Collect early feedback
- [ ] Update QUALITY_ASSURANCE.md if needed

## 🐛 Debugging Guide

### Enable Debug Mode

Add this to browser console to debug:

```javascript
// Enable verbose logging
window.DEBUG = true;

// Check animation support
console.log('SVG animations:', 
  document.querySelector('style')?.textContent?.includes('@keyframes'));

// Monitor image loading
document.querySelectorAll('img').forEach(img => {
  img.addEventListener('load', () => console.log('✓ Loaded:', img.src));
  img.addEventListener('error', () => console.log('✗ Failed:', img.src));
});

// Check external service latency
fetch('https://github-readme-stats.vercel.app/api?username=HomieB-tt')
  .then(r => console.log('Response time:', r.headers.get('date')));
```

### Common Debug Scenarios

#### Animation stuttering
```javascript
// Check frame rate
let frames = 0;
setInterval(() => {
  console.log('FPS:', frames);
  frames = 0;
}, 1000);

requestAnimationFrame(function countFrame() {
  frames++;
  requestAnimationFrame(countFrame);
});
```

#### Images not loading
```javascript
// Check all images and their status
document.querySelectorAll('img').forEach(img => {
  console.log({
    src: img.src,
    complete: img.complete,
    naturalWidth: img.naturalWidth,
    currentSrc: img.currentSrc
  });
});
```

#### Performance analysis
```javascript
// Get load metrics
const perf = window.performance.timing;
const pageLoadTime = perf.loadEventEnd - perf.navigationStart;
console.log('Page load time:', pageLoadTime, 'ms');

// Get resource timing
performance.getEntriesByType('resource').forEach(resource => {
  console.log({
    name: resource.name.split('/').pop(),
    duration: Math.round(resource.duration),
    size: resource.transferSize
  });
});
```

## 🔄 Backup & Recovery

### Creating Backup
```bash
# Backup entire profile directory
cp -r /home/buddy/Projects/HomieB-tt /home/buddy/Projects/HomieB-tt.backup

# Or just critical files
cp README.md README.md.backup
cp -r assets assets.backup
```

### Recovery Procedure
```bash
# If something goes wrong:
1. Stop all changes
2. Restore from backup:
   cp README.md.backup README.md
   cp -r assets.backup/* assets/
3. Verify restoration
4. Test thoroughly
5. Identify what went wrong
6. Fix issue
7. Test again before redeploy
```

## 📊 Status Monitoring

### External Service Status

| Service | Purpose | Status Page | Fallback |
|---------|---------|-------------|----------|
| img.shields.io | Badges | - | Local SVG |
| github-readme-stats | GitHub stats | - | stats-fallback-*.svg |
| github-readme-streak-stats | Streak counter | - | stats-fallback-streak.svg |
| GitHub (raw content) | Profile content | status.github.com | Cache |

### Monitoring Strategy

1. **Manual Check** (Weekly)
   ```bash
   # Test badge service
   curl -I https://img.shields.io/badge/test-ok-green
   
   # Test GitHub stats
   curl -I https://github-readme-stats.vercel.app/api?username=test
   ```

2. **Automated Monitoring** (Recommended)
   - Use UptimeRobot to monitor external services
   - Get alerts when services down
   - Automatic fallback activation

3. **Performance Monitoring**
   - Track load times monthly
   - Monitor Core Web Vitals
   - Alert if performance degrades >10%

## 🚨 Emergency Procedures

### If Profile Goes Down
1. Check GitHub status (status.github.com)
2. Verify all SVG files exist
3. Test with `curl README.md`
4. Check for recent commits that broke it
5. Revert to last known good version
6. Document what happened

### If External Services Fail
1. Fallback SVGs should activate automatically
2. Profile remains fully functional
3. No action needed immediately
4. Monitor service status
5. Report if service down >1 hour

### If Performance Degrades
1. Check performance metrics
2. Identify what changed
3. Review recent commits
4. Revert problematic changes
5. Test with throttled network
6. Optimize or implement workaround

## 📞 Getting Help

### Common Resources
- [SVG Reference](https://developer.mozilla.org/en-US/docs/Web/SVG)
- [CSS Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations)
- [Web Accessibility](https://www.w3.org/WAI/WCAG21/quickref/)
- [GitHub Status](https://status.github.com)

### Debug Checklist
- [ ] Verified file exists and is accessible
- [ ] Checked syntax (SVG/Markdown/CSS valid)
- [ ] Tested in multiple browsers
- [ ] Checked console for errors
- [ ] Cleared cache and tested
- [ ] Tested with reduced motion
- [ ] Tested on mobile
- [ ] Checked external service status

## 📝 Logging & Reporting

### When to Report Issues
- Broken links that don't resolve
- Images consistently failing to load
- Performance regression >20%
- Accessibility issues found
- Browser compatibility problems

### How to Report
1. Document exact issue
2. Include browser/device info
3. Provide reproduction steps
4. Include screenshot if possible
5. Note timing (when started)
6. Update QUALITY_ASSURANCE.md

### Issue Template
```
## Issue: [Brief Description]
- Severity: [Critical/High/Medium/Low]
- Browser: [Name and Version]
- Device: [Desktop/Mobile, OS]
- Reproduction: [Steps to reproduce]
- Expected: [What should happen]
- Actual: [What actually happens]
- Screenshot: [If applicable]
- Notes: [Any other relevant info]
```

---

**Last Updated**: 2024-08-14  
**Maintenance Owner**: Jeremiah Carlton  
**Emergency Contact**: montanajeremy160@outlook.com
