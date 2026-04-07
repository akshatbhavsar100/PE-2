# Disaster Analyzer - Vercel Deployment Guide

## Overview
This is a Disaster Management Budget Analyzer with ML-powered predictions, ready for deployment on Vercel.

## Features
- **Real-time Analytics**: Interactive dashboard with disaster data visualization
- **ML Predictions**: Budget and impact prediction models
- **Risk Assessment**: State-wise risk clustering
- **Responsive Design**: Modern UI with dark theme

## Project Structure
```
disaster-analyzer/
|-- api/
|   |-- index.py              # Serverless API handler
|-- disaster-analyzer/
|   |-- backend/
|   |   |-- main.py          # Original FastAPI app
|   |   |-- *.pkl            # ML models
|   |   |-- disaster.db      # SQLite database
|   |-- frontend/
|   |   |-- Untitled-1.html  # Frontend application
|-- index.html                # Main frontend file
|-- package.json              # Node dependencies
|-- requirements.txt          # Python dependencies
|-- vercel.json              # Vercel configuration
```

## Quick Deploy to Vercel

### Prerequisites
- Vercel account
- GitHub account (recommended)
- Vercel CLI (optional)

### Method 1: Vercel Web Dashboard
1. Push your code to GitHub
2. Go to [vercel.com](https://vercel.com)
3. Click "New Project"
4. Import your GitHub repository
5. Vercel will auto-detect the framework
6. Click "Deploy"

### Method 2: Vercel CLI
```bash
# Install Vercel CLI
npm i -g vercel

# Login to Vercel
vercel login

# Deploy from project root
vercel

# For production deployment
vercel --prod
```

### Method 3: Git Integration
```bash
# Install Vercel CLI
npm i -g vercel

# Link project
vercel link

# Deploy on every push
git add .
git commit -m "Deploy to Vercel"
git push origin main
```

## Environment Variables
The application works out-of-the-box with sample data. For production with real data:

1. **Database**: The app includes a SQLite database
2. **ML Models**: Models are bundled in the repository
3. **Fallback**: If database/models are missing, uses sample data

## API Endpoints
- `GET /api/states` - Get list of states
- `GET /api/disasters` - Get disaster data
- `GET /api/budget` - Get budget information
- `GET /api/predict/budget` - Predict budget requirements
- `GET /api/predict/impact` - Predict people affected
- `GET /api/health` - Health check endpoint

## Frontend Features
- **Overview Dashboard**: Key statistics and charts
- **Disaster Events**: Filterable disaster log
- **ML Predictions**: Interactive prediction interface
- **Risk Clusters**: State risk classification

## Local Development
```bash
# Install dependencies
npm install
pip install -r requirements.txt

# Run backend
cd disaster-analyzer/backend
py -m uvicorn main:app --reload --host 0.0.0.0 --port 8000

# Run frontend (separate terminal)
cd disaster-analyzer/frontend
py -m http.server 3000

# Or use Vercel dev
vercel dev
```

## Configuration Details

### vercel.json
- Configures Python runtime for serverless functions
- Routes API calls to `/api/*` to the serverless handler
- Serves frontend files from root directory

### Serverless API
- **Runtime**: Python 3.9
- **Framework**: FastAPI
- **Database**: SQLite (with sample data fallback)
- **ML Models**: Scikit-learn models with fallback calculations

### Frontend
- **Framework**: Vanilla JavaScript with Chart.js
- **Styling**: Custom CSS with dark theme
- **API Integration**: Dynamic URL configuration for dev/prod

## Troubleshooting

### Common Issues
1. **Build Failures**: Check Python version compatibility
2. **API Errors**: Verify database and model files are included
3. **CORS Issues**: Already configured in FastAPI middleware
4. **Static Files**: Ensure index.html is in root directory

### Debug Mode
Add debug logging by setting environment variable:
```bash
vercel env add DEBUG
# Set value to "true"
```

## Performance Optimization
- **Serverless**: Auto-scales based on traffic
- **Static Assets**: Served from Vercel's CDN
- **Database**: SQLite for fast reads
- **ML Models**: Pre-loaded in memory

## Monitoring
- Vercel Analytics for traffic monitoring
- Function logs for API debugging
- Error tracking through Vercel dashboard

## Custom Domain
1. Go to Vercel project settings
2. Add custom domain
3. Update DNS records
4. SSL certificate auto-provisioned

## Scaling
- **Database**: Consider migrating to PostgreSQL for large datasets
- **ML Models**: Can be updated without redeployment
- **CDN**: Automatic through Vercel's global network

## Support
For issues:
1. Check Vercel deployment logs
2. Verify all files are committed to Git
3. Test locally with `vercel dev`
4. Check API endpoints with `/api/health`

---

**Ready to deploy!** The application is fully configured for Vercel deployment with fallback data and error handling.
