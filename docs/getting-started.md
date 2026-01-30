# Getting Started

This guide will help you set up Habits Factory for local development.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Python 3.10+** - For the Django backend
- **Node.js 18+** - For the Vue.js frontend
- **npm** or **yarn** - Package manager for frontend dependencies
- **Git** - Version control

## Clone the Repository

```bash
git clone https://github.com/habitsfactory/habitsfactory-app.git
cd habitsfactory-app
```

## Backend Setup

### 1. Create a Virtual Environment

```bash
cd backend
python -m venv venv
```

Activate the virtual environment:

=== "Windows"

    ```bash
    call venv/Scripts/activate
    ```

=== "macOS/Linux"

    ```bash
    source venv/bin/activate
    ```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables

Create a `.env` file in the backend directory:

```bash
DEBUG=True
SECRET_KEY=your-secret-key-here
DATABASE_URL=sqlite:///db.sqlite3
ALLOWED_HOSTS=localhost,127.0.0.1
CORS_ALLOWED_ORIGINS=http://localhost:5173
```

### 4. Run Migrations

```bash
python manage.py migrate
```

### 5. Create a Superuser (Optional)

```bash
python manage.py createsuperuser
```

### 6. Start the Backend Server

```bash
python manage.py runserver
```

The API will be available at `http://localhost:8000`.

## Frontend Setup

### 1. Install Dependencies

Open a new terminal and navigate to the frontend directory:

```bash
cd frontend
npm install
```

### 2. Configure Environment Variables

Create a `.env` file in the frontend directory:

```bash
VITE_API_URL=http://localhost:8000/api
```

### 3. Start the Development Server

```bash
npm run dev
```

The application will be available at `http://localhost:5173`.

## Docker Setup (Coming Soon)

A Docker Compose configuration is planned for simplified setup:

```bash
# Future one-command setup
docker-compose up
```

This will provide:

- Local development environment
- Production parity
- Isolated dependencies

## Project Structure

```
habitsfactory-app/
├── backend/               # Django REST API
│   ├── api/              # API endpoints
│   ├── habits/           # Habit models and logic
│   ├── analytics/        # Correlation algorithms
│   └── manage.py
├── frontend/             # Vue.js application
│   ├── src/
│   │   ├── components/   # Vue components
│   │   ├── views/        # Page views
│   │   ├── stores/       # State management
│   │   └── api/          # Axios API client
│   ├── public/
│   └── vite.config.js
└── docker-compose.yml    # (Coming soon)
```

## Verifying the Installation

1. **Backend**: Visit `http://localhost:8000/api/` to see the API root
2. **Frontend**: Visit `http://localhost:5173` to see the application
3. **Admin**: Visit `http://localhost:8000/admin/` to access Django admin

## Troubleshooting

### CORS Errors

If you see CORS errors in the browser console:

1. Verify `CORS_ALLOWED_ORIGINS` in your backend `.env` file
2. Ensure the frontend URL matches the allowed origin
3. Restart the backend server after changes

### Database Errors

If migrations fail:

```bash
# Reset the database (development only)
rm db.sqlite3
python manage.py migrate
```

### Port Conflicts

If ports 8000 or 5173 are in use:

```bash
# Run backend on different port
python manage.py runserver 8001

# Run frontend on different port
npm run dev -- --port 3000
```

Update your `.env` files accordingly.

## Next Steps

- Read the [Architecture](architecture.md) documentation to understand the system design
- Explore [Features](features.md) to learn what Habits Factory can do
- Check the [API Reference](api-reference.md) for endpoint documentation
