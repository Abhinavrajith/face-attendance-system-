python3 -m uvicorn backend.main:app --reload --host 127.0.0.1 --port 8000
python3 -m http.server 3000 --directory frontend
