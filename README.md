# Raj Kumar Shoe Repairing backend

## Deploy the backend to Render

Create a Render Web Service for this repository and use its Docker runtime. The
Dockerfile activates the `uat` Spring profile and listens on Render's `PORT`.
The UAT profile uses PostgreSQL; local development and the `prod` profile keep
their Oracle configuration.

Add these environment variables to the Render service:

- `NEON_HOST`: Neon hostname (use the pooled hostname if using Neon pooling)
- `NEON_DATABASE`: database name
- `NEON_USERNAME` and `NEON_PASSWORD`: database credentials
- `NEON_PORT`: `5432` (optional)
- `JWT_SECRET`: private signing secret
- `ADMIN_PHONE` and `ADMIN_PASSWORD`: initial owner account credentials
- `FRONTEND_URL` and `CORS_ORIGIN`: deployed frontend origin

The database connection requires TLS. SMTP settings are optional; set
`SMTP_USERNAME` and `SMTP_PASSWORD` to enable authenticated email.

## Deploy the frontend to Render

Create a Render Static Site for the frontend repository. Set the root directory
to `frontend`, use `npm ci && npm run build` as the build command, and set
`dist` as the publish directory. Set `VITE_API` to the backend's public URL
ending in `/api` and redeploy after changing it.

## Run locally

Start Oracle locally, then run the backend from this directory with
`mvn spring-boot:run`. In the frontend repository, run `npm run dev` from its
`frontend` directory. The frontend defaults to `http://localhost:8080/api` for
the backend API.
