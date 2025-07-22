# 🚀 Deploy Travel Agent to Render

## Quick Deployment Steps

### 1. **Prepare Your Repository**
```bash
# Make sure all files are committed
git add .
git commit -m "Ready for Render deployment"
git push origin main
```

### 2. **Create Render Account**
- Go to [render.com](https://render.com) and sign up/login
- Connect your GitHub repository

### 3. **Deploy Using render.yaml (Recommended)**
- Click **"New +"** → **"Blueprint"**
- Select your repository
- Render will automatically detect `render.yaml` and deploy both services

### 4. **Manual Deployment (Alternative)**

#### Backend Service:
- **Name:** `travel-agent-backend`
- **Environment:** `Python 3`
- **Build Command:** `pip install -r backend/requirements.txt`
- **Start Command:** `cd backend && uvicorn main:app --host 0.0.0.0 --port $PORT`
- **Root Directory:** `backend`

#### Frontend Service:
- **Name:** `travel-agent-frontend`
- **Environment:** `Static Site`
- **Build Command:** `echo "Frontend ready"`
- **Publish Directory:** `frontend`

### 5. **Environment Variables**
Add these in Render dashboard → Environment:

```
OPENAI_API_KEY=your_openai_api_key_here
AMADEUS_CLIENT_ID=your_amadeus_client_id
AMADEUS_CLIENT_SECRET=your_amadeus_client_secret
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_anon_key
RENDER=true
```

### 6. **Update Frontend API URLs**
After deployment, update your frontend API calls to use the Render backend URL:

```javascript
// In frontend/js/api.js
const API_BASE_URL = 'https://your-backend-name.onrender.com';
```

### 7. **Test Your Deployment**
- Backend: `https://your-backend-name.onrender.com/docs`
- Frontend: `https://your-frontend-name.onrender.com`

## 🔧 Troubleshooting

### Common Issues:
1. **Build Fails**: Check `requirements.txt` has all dependencies
2. **CORS Errors**: Backend CORS is already configured for Render
3. **Environment Variables**: Make sure all API keys are set correctly
4. **Port Issues**: Render automatically sets `$PORT` environment variable

### Health Check:
- Backend health: `https://your-backend-name.onrender.com/api/health`
- Should return: `{"status": "healthy", "timestamp": "..."}`

## 📁 File Structure for Render
```
Travel-Agent/
├── backend/
│   ├── main.py
│   ├── requirements.txt
│   └── static/
├── frontend/
│   ├── index.html
│   ├── css/
│   └── js/
├── render.yaml
└── DEPLOYMENT.md
```

## 🎯 Final URLs
After deployment, you'll have:
- **Backend API:** `https://travel-agent-backend.onrender.com`
- **Frontend App:** `https://travel-agent-frontend.onrender.com`
- **API Docs:** `https://travel-agent-backend.onrender.com/docs`

## ✅ Success Checklist
- [ ] Repository pushed to GitHub
- [ ] Environment variables set in Render
- [ ] Backend service deployed successfully
- [ ] Frontend service deployed successfully
- [ ] API health check passes
- [ ] Frontend can connect to backend
- [ ] All features working (recommendations, flight search, etc.)
