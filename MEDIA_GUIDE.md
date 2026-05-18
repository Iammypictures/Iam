# Media Upload & Optimization Guide

## Quick Upload Instructions

Follow this guide to upload your media files optimally.

---

## 1. PROFILE PHOTO (Hero/Front Page)

### What to upload:
- Your best profile photo for the hero section
- Recommended: Professional headshot or portrait
- Should convey your brand/personality

### Technical Requirements:
- **Recommended size**: 1920 x 1080px (16:9 aspect ratio)
- **File formats to create**:
  - `hero-hero.jpg` (JPEG 80-85% quality, ~400-600KB)
  - `hero-hero.webp` (WebP, ~200-300KB)
  - `hero-hero-small.webp` (Mobile version, 768px wide, ~80-120KB)

### Optimization steps:
```bash
# Using ImageMagick or similar tools:

# Create main JPEG
convert photo.jpg -quality 85 -resize 1920x1080 hero-hero.jpg

# Create WebP (main)
cwebp -q 80 hero-hero.jpg -o hero-hero.webp

# Create mobile WebP
convert photo.jpg -resize 768x432 hero-hero-small.webp
```

### Upload location:
```
assets/images/
├── hero-hero.jpg
├── hero-hero.webp
└── hero-hero-small.webp
```

---

## 2. VIDEO (Conor/Tedani Recording)

### What to upload:
- Full video recording of the Conor/Tedani conversation
- Should be well-lit and have clear audio

### Technical Requirements:
- **Duration**: Any length (recommended under 10 minutes for web)
- **Resolution**: 1920 x 1080p (Full HD) or higher
- **Frame rate**: 24fps or 30fps
- **Audio**: Stereo mix, 128-256 kbps

### Formats to create:
```
1. MP4 (H.264 codec)
   - Codec: H.264
   - Bitrate: 2500-5000 kbps
   - Audio: AAC, 192 kbps
   - File size: 200-500MB (typical for 5-10 min video)

2. WebM (VP9 codec)
   - Codec: VP9
   - Bitrate: 1500-3000 kbps
   - Audio: Opus, 128 kbps
   - File size: 100-250MB (30-40% smaller than MP4)

3. Thumbnail/Poster
   - Format: JPEG
   - Size: 1920 x 1080px
   - Use: First frame or best scene
   - Quality: 80-85%
```

### Video Encoding Commands

**Using FFmpeg:**

```bash
# Create MP4 (H.264)
ffmpeg -i input-video.mov \
  -c:v libx264 \
  -preset slow \
  -crf 22 \
  -c:a aac \
  -b:a 192k \
  tedani-conor-recording.mp4

# Create WebM (VP9)
ffmpeg -i input-video.mov \
  -c:v libvpx-vp9 \
  -b:v 2000k \
  -c:a libopus \
  -b:a 128k \
  tedani-conor-recording.webm

# Extract thumbnail
ffmpeg -i input-video.mov \
  -ss 00:00:05 \
  -vframes 1 \
  -vf "scale=1920:1080" \
  -q:v 3 \
  video-thumbnail.jpg
```

### Upload location:
```
assets/videos/
├── tedani-conor-recording.mp4
├── tedani-conor-recording.webm
└── ../images/video-thumbnail.jpg
```

---

## 3. BEFORE & AFTER IMAGES

### What to upload:
- **Before image**: Starting point of transformation
- **After image**: Current/final state after transformation
- Can be single split image or two separate images

### Technical Requirements:
- **Aspect ratio**: 1:1 (square) or 16:9 (landscape)
- **Recommended size**: 1200 x 1200px (square)
- **File formats**:
  - JPEGs for fallback
  - WebP for primary
  - Mobile versions (768px max width)

### Creating optimized versions:

**For each image (before-after-1.jpg, before-after-2.jpg):**

```bash
# Main JPEG
convert original-image.jpg -quality 85 -resize 1200x1200 before-after-1.jpg

# Main WebP
cwebp -q 80 before-after-1.jpg -o before-after-1.webp

# Mobile JPEG
convert original-image.jpg -resize 768x768 before-after-1-small.jpg

# Mobile WebP
convert original-image.jpg -resize 768x768 before-after-1-small.webp
```

### Upload location:
```
assets/images/
├── before-after-1.jpg
├── before-after-1.webp
├── before-after-1-small.webp
├── before-after-2.jpg
├── before-after-2.webp
└── before-after-2-small.webp
```

---

## 4. ADDITIONAL DOCUMENTATION (Hospital Before Photo)

### What to upload:
- Supporting images from the journey
- Hospital photo or other documentation
- Can create a gallery of 3-5 images

### Technical Requirements:
- Same as before/after images
- Aspect ratio: 1:1 (square) recommended
- Size: 1200 x 1200px

### Creating versions:

```bash
# Main versions
convert hospital-photo.jpg -quality 85 -resize 1200x1200 hospital-before.jpg
cwebp -q 80 hospital-before.jpg -o hospital-before.webp

# Mobile versions
convert hospital-photo.jpg -resize 768x768 hospital-before-small.webp
```

### Upload location:
```
assets/images/
├── hospital-before.jpg
├── hospital-before.webp
├── hospital-before-small.webp
└── [Add more gallery images as needed]
```

---

## File Size Targets

| File Type | Target Size | Quality |
|-----------|------------|---------|
| Hero JPEG | 400-600 KB | 85% quality |
| Hero WebP | 200-300 KB | 80% quality |
| Hero Mobile WebP | 80-120 KB | Mobile optimized |
| Before/After JPEG | 150-300 KB | 85% quality |
| Before/After WebP | 80-150 KB | 80% quality |
| Mobile Before/After WebP | 40-60 KB | Mobile optimized |
| Video Thumbnail JPEG | 100-150 KB | 85% quality |
| MP4 Video | 200-500 MB | 2500-5000 kbps bitrate |
| WebM Video | 100-250 MB | 1500-3000 kbps bitrate |

---

## Tools Recommended for Optimization

### Image Optimization
- **TinyPNG** (https://tinypng.com) - Easy online compression
- **ImageOptim** (https://imageoptim.com) - Mac desktop app
- **Squoosh** (https://squoosh.app) - Google's web optimizer
- **ImageMagick** (https://imagemagick.org) - Command line powerhouse

### Video Encoding
- **FFmpeg** (https://ffmpeg.org) - Best for batch processing
- **HandBrake** (https://handbrake.fr) - User-friendly GUI
- **CloudConvert** (https://cloudconvert.com) - Online converter
- **Adobe Media Encoder** - Professional option

### Online Converters
- **CloudConvert.com** - Formats: WebP, JPEG, WebM, MP4, etc.
- **Online-Convert.com** - Free converter for any format
- **Convertio.co** - Batch processing available

---

## Step-by-Step Upload Process

### 1. Optimize Your Media
```bash
# Process all images and videos locally first
# Use tools mentioned above to compress

# Verify file sizes are within targets
ls -lh assets/images/*
ls -lh assets/videos/*
```

### 2. Upload to GitHub

**Option A: Web Interface**
1. Go to: https://github.com/Iammypictures/Iam
2. Click "Add file" → "Upload files"
3. Navigate to `assets/images/` or `assets/videos/`
4. Drag and drop your optimized files
5. Add commit message: "Add optimized media assets"
6. Commit

**Option B: Git Command Line**
```bash
# Clone repo (if not already)
git clone https://github.com/Iammypictures/Iam.git
cd Iam

# Copy your optimized files to assets/
cp ~/optimized-images/* assets/images/
cp ~/optimized-videos/* assets/videos/

# Add, commit, push
git add assets/
git commit -m "Add optimized media assets (images and video)"
git push origin main
```

### 3. Verify Everything Works
1. Open https://iammypictures.github.io/Iam (or your GitHub Pages URL)
2. Check that:
   - Hero image loads and displays properly
   - Video plays with poster thumbnail
   - Before/After images display in gallery
   - All images load quickly
   - Responsive on mobile devices

---

## Performance Checklist

- [ ] All images compressed to recommended file sizes
- [ ] WebP versions created for all images
- [ ] Mobile-optimized versions created
- [ ] Video files encoded (MP4 and WebM)
- [ ] Video thumbnail created
- [ ] Files uploaded to correct `assets/` directories
- [ ] Website loads in < 2 seconds on 4G
- [ ] Images scale properly on mobile
- [ ] Video plays smoothly
- [ ] No console errors in DevTools

---

## Troubleshooting

### Images not showing
- Check file paths match exactly (case-sensitive on Linux/Mac)
- Verify files are in `assets/images/` directory
- Clear browser cache (Ctrl+Shift+Del)

### Video won't play
- Ensure both MP4 and WebM formats are uploaded
- Check video codec (H.264 for MP4, VP9 for WebM)
- Test in Chrome first (most compatible)

### Page loads slowly
- Verify images are WebP format where possible
- Check image file sizes against targets
- Ensure video is properly encoded
- Use Google Lighthouse to identify issues

### Mobile looks wrong
- Verify mobile image variants exist
- Test on real device or Chrome DevTools
- Check CSS media queries are working

---

## Next Steps

1. **Gather your media files** (video, photos)
2. **Optimize using tools above** (compress, resize, convert)
3. **Upload to GitHub** following the upload process
4. **Test the website** on various devices
5. **Monitor performance** with Google Lighthouse
6. **Share your portfolio** with the world!

For detailed performance optimization, see README.md.
