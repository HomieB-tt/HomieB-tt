# Quick Reference Card

## 📋 One-Page Cheat Sheet for Profile Management

### 🎯 Most Common Tasks

#### Updating Project Status
1. Open README.md → Find "## 🚀 FEATURED PROJECTS"
2. Update status badges (🟢 Active, 🟡 Maintaining, ⚠️ Archived)
3. Update project description if needed
4. Test links still work

#### Changing Tech Stack
1. Open README.md → Find "## 🛠️ TECH STACK"
2. Add/remove technology badges
3. Update descriptions
4. Verify formatting consistency

#### Updating Learning Progress
1. Open README.md → Find "## 📚 LEARNING TRAJECTORY"
2. Update Progress column (🟢 80%, 🟡 60%, 🟠 25%, etc.)
3. Add/remove learning topics
4. Maintain table structure

#### Fixing Broken Links
1. Check QUALITY_ASSURANCE.md for verified links
2. Update URL in README.md
3. Test link works before deploying
4. Document change

### 🎨 Design Updates

#### Changing Colors
1. Reference DESIGN_SYSTEM.md for current palette
2. Update hex codes in:
   - SVG files (profile-hero.svg, profile-footer.svg)
   - README.md inline styles if any
3. Update DESIGN_SYSTEM.md with new palette
4. Test contrast ratios (min 4.5:1 for text)

#### Adding Animations
1. Check DESIGN_SYSTEM.md animation guidelines
2. Add `@keyframes` to SVG `<style>` section
3. Apply to element with animation class
4. Test smooth 60fps performance
5. Add static fallback

#### Updating SVG Assets
1. Edit asset in assets/ directory
2. Keep file size <10KB
3. Maintain color palette
4. Verify animations work
5. Update DESIGN_SYSTEM.md if needed

### ✅ Testing Checklist

#### Before Deployment
- [ ] All links tested and working
- [ ] SVGs render correctly
- [ ] Animations smooth (60fps)
- [ ] Mobile responsive (320px tested)
- [ ] Contrast ratios verified (4.5:1+)
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] No typos or grammar errors

#### Post-Deployment
- [ ] View live on GitHub
- [ ] Test on mobile device
- [ ] Check with screen reader
- [ ] Verify animations play
- [ ] Confirm fallbacks work

### 🔍 Quick Diagnostics

#### SVG Not Displaying
```bash
# Check file exists
ls -l assets/filename.svg

# Validate syntax
xmllint --noout assets/filename.svg
```

#### Animations Not Working
```javascript
// Paste in browser console
document.querySelectorAll('style').forEach(s => {
  console.log('Animation rules:', s.textContent);
});
```

#### Performance Slow
```javascript
// Paste in browser console to check load times
performance.getEntriesByType('resource').forEach(r => {
  console.log(r.name.split('/').pop(), Math.round(r.duration) + 'ms');
});
```

#### Links Broken
```bash
# Check specific link
curl -I https://github.com/HomieB-tt

# Find broken links (requires linkchecker)
linkchecker README.md
```

### 📁 File Reference

| File | Purpose | Edit When |
|------|---------|-----------|
| README.md | Main profile content | Updating any profile info |
| profile-hero.svg | Top banner | Changing design/header |
| profile-footer.svg | Bottom banner | Changing footer |
| stats-fallback-*.svg | Offline stats | Stats display format changes |
| DESIGN_SYSTEM.md | Design standards | Adding new design elements |
| QUALITY_ASSURANCE.md | Testing checklist | After major changes |
| PERFORMANCE.md | Optimization guide | Performance issues |
| TROUBLESHOOTING.md | Support guide | Issues arise |

### 🚀 Quick Deploy Workflow

```bash
# 1. Make changes to file
nano README.md

# 2. Verify locally
cat README.md | head -50

# 3. Check all assets exist
ls -la assets/

# 4. Verify links
grep -o "https://[^[:space:])]\\+" README.md

# 5. Commit and push
git add .
git commit -m "Update profile: [description]"
git push origin main

# 6. View live
# https://github.com/HomieB-tt (wait ~30 seconds for render)
```

### ⚡ Performance Tips

- **Keep SVGs <10KB** - Use SVGO to optimize
- **Animations <800ms** - User attention span
- **Reduce simultaneous animations** - Max 3-4 at once
- **Use transform & opacity** - GPU accelerated
- **Avoid width/height changes** - Use transform instead
- **Cache aggressively** - Assets reuse often

### ♿ Accessibility Checklist (Quick)

- [ ] Text contrast 4.5:1+ (use WebAIM tool)
- [ ] No information by color alone
- [ ] Keyboard navigation works (Tab through)
- [ ] Focus indicators visible
- [ ] Images have alt text
- [ ] Links describe destination
- [ ] Animations respect prefers-reduced-motion
- [ ] No flashing >3 times/second

### 🎨 Color Quick Reference

```
Primary:      #22D3EE (Cyan)
Secondary:    #8B5CF6 (Purple)
Tertiary:     #EC4899 (Pink)
Accent:       #14B8A6 (Teal)

Background:   #050816 (Dark)
Text:         #F8FAFC (Bright)
Secondary:    #CBD5E1 (Medium)
Tertiary:     #94A3B8 (Dim)
```

### 🔄 External Services Status

| Service | When Down | Fallback |
|---------|-----------|----------|
| img.shields.io | Badge broken | Local stats SVG |
| github-readme-stats | Stats missing | stats-fallback-*.svg |
| GitHub raw | Content missing | Cache activated |

### 📞 Get Help

1. **Design question?** → Read DESIGN_SYSTEM.md
2. **Something broken?** → Check TROUBLESHOOTING.md
3. **Performance issue?** → See PERFORMANCE.md
4. **Need to verify?** → Use QUALITY_ASSURANCE.md
5. **Want context?** → Review ENHANCEMENT_SUMMARY.md

### 🎯 Monthly Maintenance (5 min)

```bash
# 1. Check performance
# → Open DevTools, run Lighthouse

# 2. Verify links (weekly actually)
# → Click 2-3 random links

# 3. Check animations
# → Reload page, verify smooth

# 4. Mobile test
# → Open on phone, scroll through
```

### 💡 Pro Tips

1. **Batch edits** - Make multiple changes at once
2. **Test early** - Don't wait until deployment
3. **Use fallbacks** - Always provide static versions
4. **Document changes** - Update docs when you change design
5. **Monitor performance** - Monthly Lighthouse runs
6. **Keep it simple** - Don't overcomplicate the design
7. **Respect motion preferences** - Test with reduced motion enabled
8. **Stay consistent** - Reference DESIGN_SYSTEM.md

### 🚨 Emergency Procedures

**Profile won't load?**
1. Check GitHub status (status.github.com)
2. Force refresh (Ctrl+Shift+R)
3. Check assets directory exists
4. Verify no uncommitted changes

**Links all broken?**
1. Check GitHub account still exists
2. Verify URLs in README.md
3. Test links individually
4. Update and re-commit

**Animations frozen?**
1. Check browser supports CSS animations
2. Clear cache
3. Try different browser
4. Check animation syntax (see DESIGN_SYSTEM.md)

### 📊 File Sizes (Keep These in Mind)

```
Profile-hero.svg:          ~8KB  (Keep under 10KB)
Profile-footer.svg:        ~6KB  (Keep under 8KB)
Stats fallback SVGs:        ~1-3KB each
README.md:                  ~14KB (Keep under 20KB)
Total profile size:         ~120KB (Keep under 500KB)
```

### 🎓 Learning Resources

- **Design**: DESIGN_SYSTEM.md (complete reference)
- **Testing**: QUALITY_ASSURANCE.md (checklist)
- **Performance**: PERFORMANCE.md (optimization guide)
- **Troubleshooting**: TROUBLESHOOTING.md (solutions)
- **Context**: ENHANCEMENT_SUMMARY.md (overview)

---

## Quick Links

| Resource | Location | Purpose |
|----------|----------|---------|
| Design Standards | DESIGN_SYSTEM.md | Reference for all design decisions |
| QA Checklist | QUALITY_ASSURANCE.md | Verify everything works |
| Performance Guide | PERFORMANCE.md | Optimization techniques |
| Support & Debugging | TROUBLESHOOTING.md | Fix issues |
| Enhancement Details | ENHANCEMENT_SUMMARY.md | Understand what changed |
| Main Profile | README.md | What visitors see |
| Assets | assets/ | SVG graphics and fallbacks |

---

**Bookmark this page for quick reference!**  
**Print version available in TROUBLESHOOTING.md**  
**Last updated**: 2024-08-14
