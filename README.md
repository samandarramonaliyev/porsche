# Porsche 911 Configurator Platform

Production-ready full-stack Porsche 911 configurator with real-time 3D rendering,
dynamic pricing, and order persistence.

## Project structure

```
backend/
  src/
    config/
    controllers/
    models/
    routes/
    server.js
frontend/
  public/
    models/
    sitemap.xml
  src/
    api/
    components/
    pages/
    store/
    utils/
```

## Quick start

### Frontend
```
cd frontend
npm install
npm run dev
```

### Backend
```
cd backend
npm install
npm run dev
```

## Environment variables

Frontend (`frontend/.env`):
```
VITE_API_URL=http://localhost:5000
```

Backend (`backend/.env`):
```
PORT=5000
MONGO_URI=mongodb+srv://USER:PASS@cluster.mongodb.net/porsche-configurator
CORS_ORIGIN=http://localhost:5173
```

## Replacing the 3D model

1. Place the new model at `frontend/public/models/porsche_911.glb`.
2. Ensure mesh names include clear keywords like `body`, `rim`, `wheel`, or `interior` for
   auto material assignment.
3. If the model uses different naming, update the name matching logic in
   `frontend/src/components/CarCanvas.jsx`.

## Export optimized .glb from Blender

1. **Clean scene**: Remove unused objects/materials, apply transforms (`Ctrl+A`).
2. **Reduce geometry**: Use Decimate modifier or manually retopologize where possible.
3. **Bake textures**: Pack or bake textures to reduce draw calls.
4. **Use glTF exporter**:
   - Format: `glTF Binary (.glb)`
   - Include: Meshes, Materials, Textures
   - Compression: Enable Draco (if available) for geometry.
5. **Test in viewer**: Use https://gltf-viewer.donmccurdy.com/ to verify materials and scale.

## Deployment

### Frontend → Vercel
1. Import `frontend` as a Vercel project.
2. Set build command: `npm run build`
3. Output directory: `dist`
4. Set `VITE_API_URL` to your backend URL.

### Backend → Render / Railway
1. Create a new Node.js service from `backend`.
2. Set start command: `npm run start`
3. Add environment variables (`MONGO_URI`, `CORS_ORIGIN`, `PORT`).
4. Allow inbound traffic on `PORT` (Render/Railway handles this automatically).

## Notes

- Place a social cover image at `frontend/public/og-cover.jpg` for OpenGraph.
- Update `frontend/public/sitemap.xml` with your production domain.
