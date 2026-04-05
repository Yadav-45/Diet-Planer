# Frontend-Backend Integration Guide

## Current Setup

### Frontend (Vite React)
- **Port:** 5174 (or next available if busy)
- **Dev Server:** http://localhost:5174
- **Running:** ✅ (via `npm run dev`)

### Backend (Express/Node.js)
- **Port:** 8080
- **Expected URL:** http://localhost:8080
- **Google API Key:** Configured in `.env`

### Proxy Configuration
The Vite dev server automatically proxies all `/api/*` requests to the backend:
```
http://localhost:5174/api/scan → http://localhost:8080/api/scan
http://localhost:5174/api/nutrition → http://localhost:8080/api/nutrition
http://localhost:5174/api/meal-plan → http://localhost:8080/api/meal-plan
```

## Testing the Integration

### 1. Start Backend (if not running)
```powershell
# Set environment variables
$env:GOOGLE_API_KEY = "AIzaSyDm3ROFyv7EdICGUyUc7Sv2_nBttQOYWbs"
$env:PORT = "8080"

# Run backend (replace with your backend start command)
npm run dev:api
# or
node server.js
```

### 2. Frontend is Already Running
```powershell
# Terminal output shows:
VITE v5.4.19  ready in 574 ms
➜  Local:   http://localhost:5174/
```

### 3. Test the Integration

#### Option A: Manual Test via Browser
1. Open http://localhost:5174/ in your browser
2. Navigate to "Scan" page
3. Upload an image
4. Click "Scan" button
5. Check browser console (F12 → Console) for:
   - Request to `/api/scan`
   - Response from backend
   - Toast notification with results

#### Option B: Test via API
```powershell
# Test if backend is reachable from frontend dev server
$response = Invoke-WebRequest -Uri "http://localhost:5174/api/scan" `
  -Method POST `
  -Headers @{"Content-Type" = "application/json"} `
  -Body '{"test": "data"}'

Write-Host $response.StatusCode
Write-Host $response.Content
```

## API Endpoints

### 1. Scan Food Image
- **Endpoint:** `POST /api/scan`
- **Input:** FormData with `image` file
- **Output:** JSON with food detection results
- **Used in:** ScanFood page

### 2. Get Nutrition Info
- **Endpoint:** `GET /api/nutrition?food=<name>`
- **Input:** Food name as query parameter
- **Output:** JSON with nutritional data
- **Used in:** Results, Plan pages

### 3. Generate Meal Plan
- **Endpoint:** `POST /api/meal-plan`
- **Input:** JSON with user preferences
- **Output:** JSON with meal plan
- **Used in:** Plan page

## Frontend Components Using Backend

### ScanFood Page (`src/pages/ScanFood.tsx`)
- Imports `scanFoodImage` from `@/lib/api`
- Sends image file to backend `/api/scan`
- Displays results via toast notification

### API Service (`src/lib/api.ts`)
- `scanFoodImage(file)` - Upload image for scanning
- `getNutritionInfo(foodName)` - Fetch nutrition data
- `generateMealPlan(preferences)` - Generate meal plan

## Troubleshooting

### Backend not responding
- **Check:** Is backend running on port 8080?
- **Fix:** Start backend with correct PORT and GOOGLE_API_KEY
- **Verify:** `netstat -ano | findstr :8080` (shows process on port 8080)

### CORS errors
- **Check:** Vite proxy is configured correctly (see vite.config.ts)
- **Fix:** Ensure `/api` proxy target is `http://localhost:8080`
- **Note:** Proxy handles CORS automatically in dev mode

### Requests fail but no error
- **Check:** Browser Network tab (F12 → Network)
- **Look for:** Requests to `/api/scan` and their responses
- **Debug:** Check backend logs for errors

### Port already in use
- **Check:** `netstat -ano | findstr :5174` or `:8080`
- **Fix:** Kill process with `taskkill /PID <PID> /F`
- **Or:** Change Vite port in `vite.config.ts`

## Environment Variables

### `.env` (Already Configured)
```properties
GOOGLE_API_KEY=AIzaSyDm3ROFyv7EdICGUyUc7Sv2_nBttQOYWbs
PORT=8080
```

### Frontend Development
- No additional env vars needed
- Proxy configuration in `vite.config.ts` handles routing

## Next Steps

1. ✅ Frontend running on http://localhost:5174
2. ✅ Vite proxy configured
3. ⏳ Verify backend is running on port 8080
4. ⏳ Test Scan page with image upload
5. ⏳ Check browser console for successful API calls
