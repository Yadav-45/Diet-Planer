# 📷 Webcam Food Detection - User Guide

## ✨ New Features Added

### 1. **Dual Input Methods**
- **📤 Upload Tab**: Choose existing images from your device
- **📷 Camera Tab**: Capture food in real-time using your device camera

### 2. **Camera Capabilities**
- ✅ Real-time video preview
- ✅ High-quality frame capture (JPEG 0.9 quality)
- ✅ Mobile-friendly (uses rear camera on mobile devices)
- ✅ Error handling for permission denied
- ✅ Automatic stream cleanup

### 3. **New Hook: `useWebcam`**
Located in `src/hooks/use-webcam.ts`
- Manages camera permissions
- Handles video streaming
- Captures frames as image files
- Provides error states

---

## 🚀 How to Use

### **Upload Mode** (Existing)
1. Open http://localhost:5174/scan
2. Click "📤 Upload" tab (default)
3. Click "📤 Choose File"
4. Select image from device
5. Click "🔍 Analyze Food"

### **Camera Mode** (New!)
1. Open http://localhost:5174/scan
2. Click "📷 Camera" tab
3. Click "Start Camera"
4. Allow camera permission (browser will ask)
5. Point camera at food
6. Click "📸 Capture" to take photo
7. Click "🔍 Analyze Food" to scan

---

## 🔧 Technical Details

### Permission Handling
```typescript
// Browser will request permission:
// "Allow [site] to use your camera?"
// - Allow: Camera starts
// - Deny: Error message shown
```

### Camera Stream
- **Video:** 1280x720 ideal resolution
- **Audio:** Disabled
- **Mobile:** Uses rear/environment camera
- **Desktop:** Uses default camera

### Frame Capture
1. Captures current video frame
2. Draws to canvas
3. Converts to JPEG (90% quality)
4. Creates File object
5. Sent to backend for analysis

---

## 📊 UI Flow

```
┌─────────────────────────────────────┐
│       Scan Food Page                │
├─────────────────────────────────────┤
│  [📤 Upload]  [📷 Camera]           │
├─────────────────────────────────────┤
│                                     │
│  Upload Mode:                       │
│  ┌─────────────────────────────┐   │
│  │   Image Preview / Upload    │   │
│  └─────────────────────────────┘   │
│  [📤 Choose File] [✕ Clear]        │
│                                     │
│  OR                                 │
│                                     │
│  Camera Mode:                       │
│  ┌─────────────────────────────┐   │
│  │   Video Stream from Camera  │   │
│  └─────────────────────────────┘   │
│  [📸 Capture] [Stop]               │
│                                     │
│  [🔍 Analyze Food] (Appears when   │
│                     image selected) │
├─────────────────────────────────────┤
│   Nutrition Results (Right Panel)   │
│   Shows: Food, Calories, Macros... │
└─────────────────────────────────────┘
```

---

## ⚠️ Browser Support & Permissions

### Supported Browsers
- ✅ Chrome/Chromium (50+)
- ✅ Firefox (55+)
- ✅ Safari (15+)
- ✅ Edge (79+)
- ⚠️ Mobile browsers (most modern)

### Permission Requirements
- **Desktop**: Must have a webcam connected
- **Mobile**: Phone must have rear camera
- **HTTPS**: Some browsers require secure connection for production
- **User Action**: Permission must be explicitly granted

### Permission Errors
```
❌ "Camera permission denied"
   → Allow in browser settings: Settings → Privacy → Camera

❌ "No camera device found"
   → Check if camera is connected/enabled

❌ "Your browser does not support webcam access"
   → Use a modern browser (Chrome, Firefox, Safari, Edge)
```

---

## 🎯 Use Cases

### 1. **At Restaurant**
- Quickly scan dishes with camera
- Get instant nutrition info
- No need to upload/transfer files

### 2. **At Grocery Store**
- Scan packaged foods
- Check nutritional values
- Compare options in real-time

### 3. **Home Cooking**
- Check meals while preparing
- Track nutrition intake
- Share results with family

### 4. **Meal Planning**
- Scan multiple foods during meal prep
- Build meal plans based on actual foods
- Track daily nutrition

---

## 🐛 Troubleshooting

### **Camera Not Starting**
**Problem**: Click "Start Camera" but nothing happens
- Check browser permissions (check URL bar)
- Try refreshing page
- Verify camera is connected
- Try different browser

### **Blurry Capture**
**Problem**: Captured image is blurry
- Hold camera steady for 2 seconds before capturing
- Ensure good lighting
- Move closer to food (10-20cm ideal)
- Reduce motion

### **Camera Permission Prompt Not Showing**
**Problem**: No permission dialog appears
- Check if permission was previously denied:
  - Chrome: Settings → Privacy → Camera → Blocked sites
  - Firefox: Options → Privacy → Permissions → Camera
- Clear site data and try again
- Try in incognito/private mode

### **Can't Select Both Upload & Camera**
**Note**: This is intentional - tabs switch mode
- Upload mode: Upload existing images
- Camera mode: Real-time capture
- Switch tabs to change modes

---

## 📱 Mobile Experience

### iPhone/iPad
- Tap "📷 Camera" tab
- Tap "Start Camera"
- Grant permission
- Rear camera activates
- Point at food and tap "📸 Capture"

### Android
- Tap "📷 Camera" tab
- Tap "Start Camera"
- Grant permission
- Rear camera activates
- Point at food and tap "📸 Capture"

### Tips
- Ensure good lighting
- Keep phone steady
- Frame food in center
- Wait for 2 seconds before capturing

---

## 🎨 UI Components Used

- **Tabs**: Switch between Upload/Camera modes
- **Card**: Contain upload/camera sections
- **Button**: Controls (Start, Capture, Stop, Scan)
- **Alert**: Show error messages
- **Progress**: Display confidence score
- **Icons**: Visual indicators (Flame, Egg, Droplet, Wheat, Camera)

---

## 📞 Support

If camera isn't working:

1. **Check browser console** (F12 → Console)
   - Look for JavaScript errors
   - Copy error message for debugging

2. **Check camera permissions**
   - Browser settings → Camera
   - Verify site is allowed

3. **Test camera**
   - Open browser's video call feature
   - Verify camera works there first

4. **Try alternative mode**
   - If camera fails, use upload mode
   - Both methods send to same backend

---

## 📝 Next Steps

- ✅ Webcam access implemented
- ✅ Real-time video capture
- ✅ Frame to image conversion
- ⏳ Add photo filters (optional)
- ⏳ Add frame guides for better composition
- ⏳ Add batch capture mode

---

**Generated:** November 12, 2025
**Status:** Ready to Use ✅
**Devices Supported:** Desktop, Tablet, Mobile
