# 🎓 Face Recognition Attendance System

An AI-powered attendance management system using facial recognition technology. Built with FastAPI backend and vanilla JavaScript frontend.

## 📁 Project Structure

```
face-attendance-system/
├── backend/
│   ├── main.py              # FastAPI application with all endpoints
│   ├── users.json           # Registered users database
│   └── attendance.json      # Attendance records
├── frontend/
│   └── index.html           # Single-page web application
├── requirements.txt         # Python dependencies
└── README.md               # Project documentation
```

## 🚀 Features

- **User Registration**: Register new users with face capture and embedding storage
- **Attendance Marking**: Automatic face recognition for attendance tracking
- **Real-time Camera**: Live video feed with face detection
- **Data Export**: Export attendance records to Excel format
- **RESTful API**: Complete API with FastAPI documentation
- **Modern UI**: Responsive design with gradient backgrounds and animations

## 🛠️ Technology Stack

### Backend
- **FastAPI**: Modern Python web framework
- **DeepFace**: Deep learning face recognition library
- **Facenet512**: Face embedding model for accurate recognition
- **OpenCV**: Image processing
- **Pillow**: Image manipulation
- **OpenPyXL**: Excel file generation

### Frontend
- **HTML5**: Structure and video capture
- **CSS3**: Modern styling with gradients and animations
- **JavaScript**: Camera handling and API integration
- **MediaDevices API**: Webcam access

## 📋 Prerequisites

- Python 3.8 or higher
- Webcam/Camera
- Modern web browser (Chrome, Firefox, Safari, Edge)

## 🔧 Installation

1. **Clone the repository**
```bash
git clone <repository-url>
cd face-attendance-system
```

2. **Install Python dependencies**
```bash
pip3 install -r requirements.txt
```

## 🎯 Running the Application

### Start Backend Server
Open Terminal 1:
```bash
python3 -m uvicorn backend.main:app --reload --host 127.0.0.1 --port 8000
```

### Start Frontend Server
Open Terminal 2:
```bash
python3 -m http.server 3000 --directory frontend
```

### Access the Application
- **Frontend**: http://localhost:3000
- **Backend API**: http://127.0.0.1:8000
- **API Documentation**: http://127.0.0.1:8000/docs

## 📖 Implementation Details

### Backend Architecture

#### 1. **Face Recognition Pipeline**
```python
# Registration Flow
1. Capture face image from camera
2. Extract 512-dimensional face embedding using Facenet512
3. Store embedding with user details in users.json
4. Return success response

# Attendance Flow
1. Capture face image from camera
2. Extract face embedding
3. Compare with all registered embeddings using Euclidean distance
4. Find best match (minimum distance)
5. If distance < threshold (10), mark attendance
6. Store record with timestamp in attendance.json
```

#### 2. **API Endpoints**

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Health check |
| POST | `/register` | Register new user with face |
| POST | `/mark-attendance` | Mark attendance via face recognition |
| GET | `/users` | Get all registered users |
| GET | `/attendance` | Get all attendance records |
| GET | `/attendance/export` | Export attendance to Excel |

#### 3. **Data Storage**

**users.json**
```json
[
  {
    "name": "John Doe",
    "student_id": "12345",
    "embedding": [0.123, -0.456, ...] // 512 dimensions
  }
]
```

**attendance.json**
```json
[
  {
    "name": "John Doe",
    "student_id": "12345",
    "time": "2025-11-15 10:30:45"
  }
]
```

#### 4. **Face Recognition Algorithm**
- **Model**: Facenet512 (pre-trained on VGGFace2)
- **Embedding Size**: 512 dimensions
- **Distance Metric**: Euclidean distance (L2 norm)
- **Recognition Threshold**: 10.0
- **Detection**: enforce_detection=False for flexibility

### Frontend Architecture

#### 1. **Camera Integration**
```javascript
// Access user's webcam
navigator.mediaDevices.getUserMedia({ video: { facingMode: 'user' } })
  .then(stream => video.srcObject = stream)
```

#### 2. **Image Capture Process**
```javascript
1. Create canvas element
2. Mirror image horizontally (match user view)
3. Draw video frame to canvas
4. Convert to JPEG blob
5. Send to backend via FormData
```

#### 3. **UI Components**
- **Video Container**: Live camera feed with overlay
- **Status Indicator**: Shows camera active status
- **Input Fields**: Name and Student ID for registration
- **Action Buttons**: Register and Mark Attendance
- **Message Display**: Success/error feedback with animations

#### 4. **Error Handling**
- Camera permission denied
- Network connection errors
- Face not detected
- Face not recognized
- Missing input validation

## 🔐 Security Considerations

- CORS enabled for all origins (configure for production)
- Face embeddings stored instead of raw images
- Client-side input validation
- Server-side error handling

## 📊 Performance

- **Registration Time**: ~2-3 seconds
- **Recognition Time**: ~1-2 seconds
- **Embedding Extraction**: ~1 second
- **Comparison Speed**: O(n) where n = number of registered users

## 🎨 UI Features

- Gradient background with floating animations
- Glass-morphism effect on container
- Responsive design for mobile devices
- Real-time status indicators
- Smooth transitions and hover effects
- Loading states during processing

## 🔄 Workflow

### Registration Workflow
1. User enters name and student ID
2. User clicks "Register User"
3. System captures face from camera
4. Backend extracts face embedding
5. Embedding stored with user details
6. Success message displayed

### Attendance Workflow
1. User clicks "Mark Attendance"
2. System captures face from camera
3. Backend extracts face embedding
4. System compares with all registered faces
5. Best match identified (if within threshold)
6. Attendance record created with timestamp
7. Success message with user name displayed

## 📝 Future Enhancements

- [ ] Multiple face detection in single frame
- [ ] Live attendance dashboard
- [ ] User authentication and roles
- [ ] Database integration (PostgreSQL/MongoDB)
- [ ] Mobile app version
- [ ] Attendance reports and analytics
- [ ] Email notifications
- [ ] Face liveness detection
- [ ] Batch registration via CSV
- [ ] Attendance history per user

## 🐛 Troubleshooting

**Camera not working**
- Check browser permissions
- Ensure HTTPS or localhost
- Try different browser

**Face not recognized**
- Ensure good lighting
- Face camera directly
- Register with clear face image
- Adjust recognition threshold in code

**Server connection error**
- Verify backend is running on port 8000
- Check CORS settings
- Ensure correct API URL in frontend

## 📄 License

This project is open source and available under the MIT License.

## 👥 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Contact

For questions or support, please open an issue in the repository.

---

**Built with ❤️ using FastAPI and DeepFace**
