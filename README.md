# AI Workout Rep Counter with Form Analysis

An intelligent computer vision system that counts workout repetitions and analyzes your form in real-time using pose estimation.

## Features

### 🏋️ Supported Exercises
- **Squats** - Tracks knee angle and depth
- **Push-ups** - Monitors elbow angle and body alignment
- **Bicep Curls** - Measures arm movement and elbow stability

### 🎯 Key Capabilities

1. **Automatic Rep Counting**
   - Uses motion analysis to detect complete repetitions
   - Tracks movement stages (up/down)
   - Real-time counter display

2. **Form Analysis**
   - Analyzes exercise form in real-time
   - Provides instant feedback on common mistakes
   - Calculates form score (0-100%)

3. **Visual Feedback**
   - Live pose skeleton overlay
   - Joint angle measurements
   - Form score and feedback messages
   - Exercise statistics

## Technology Stack

- **OpenCV** - Video capture and image processing
- **MediaPipe** - Pose estimation and landmark detection
- **NumPy** - Mathematical calculations and angle computation

## Installation

### Prerequisites
- Python 3.8 or higher
- Webcam

### Setup Steps

1. Clone or download this project

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the application:
```bash
python workout_rep_counter.py
```

## How to Use

### Starting the Application

1. Run the script - your webcam will activate
2. Position yourself so your full body is visible in the frame
3. Select an exercise using keyboard controls
4. Start your workout!

### Keyboard Controls

- **S** - Switch to Squats
- **P** - Switch to Push-ups
- **B** - Switch to Bicep Curls
- **R** - Reset rep counter
- **Q** - Quit application

### Exercise Guidelines

#### Squats
- Stand with feet shoulder-width apart
- Face the camera sideways for best tracking
- Squat down until knees are at ~90 degrees
- Return to standing position
- Watch for form feedback: knee position, back alignment, depth

#### Push-ups
- Position yourself sideways to the camera
- Start in plank position
- Lower body until elbows are at ~90 degrees
- Push back up to starting position
- Watch for: body alignment, elbow position

#### Bicep Curls
- Stand facing the camera
- Keep elbows stationary at your sides
- Curl weight up to shoulder level
- Lower back down with control
- Watch for: elbow movement, full range of motion

## How It Works

### Pose Estimation
The system uses MediaPipe Pose to detect 33 body landmarks in real-time:
- Shoulders, elbows, wrists
- Hips, knees, ankles
- And more...

### Rep Counting Algorithm

1. **Angle Calculation**: Measures angles between three joint points
2. **Stage Detection**: Identifies "up" and "down" positions based on angle thresholds
3. **Rep Increment**: Counts a rep when transitioning from "down" to "up"

### Form Analysis

The system checks multiple form criteria:

**Squats:**
- Knee alignment (not going past toes)
- Back straightness
- Squat depth

**Push-ups:**
- Body alignment (plank position)
- Elbow position (not too wide)
- Descent depth

**Bicep Curls:**
- Elbow stability
- Full range of motion

## Output Display

The live video shows:
- Pose skeleton overlay
- Current exercise type
- Rep count
- Current stage (up/down)
- Joint angle measurement
- Form score percentage
- Real-time form feedback

## Workout Statistics

When you quit the application, you'll see:
- Total reps completed
- Average form score
- Exercise performed

## Customization

You can easily extend this project:

### Add New Exercises

```python
def analyze_new_exercise_form(self, landmarks):
    """Add your custom form analysis"""
    feedback = []
    form_score = 100
    # Add your logic here
    return feedback, form_score

def count_new_exercise_reps(self, landmarks):
    """Add your custom rep counting logic"""
    # Calculate relevant angle
    # Detect stages
    # Count reps
    return angle
```

### Adjust Thresholds

Modify angle thresholds in the counting functions:
```python
# For squats
if angle < 90:  # Change this value
    self.stage = "down"
```

### Change Form Scoring

Adjust deductions in form analysis:
```python
if knee[0] > ankle[0] + 0.05:
    form_score -= 20  # Adjust penalty
```

## Performance Tips

1. **Good Lighting** - Ensure your workout area is well-lit
2. **Camera Position** - Place camera at waist height, 6-8 feet away
3. **Full Body Visible** - Keep your entire body in frame
4. **Sideways Angle** - Face sideways for squats and push-ups
5. **Solid Background** - Plain background helps with pose detection

## Troubleshooting

**Camera won't open:**
- Check if another application is using the webcam
- Try changing camera index: `cv2.VideoCapture(1)` or `(2)`

**Poor detection:**
- Improve lighting
- Wear contrasting clothing
- Remove clutter from background

**Inaccurate counting:**
- Perform slower, controlled reps
- Ensure full range of motion
- Check camera angle and distance

**Low FPS:**
- Close other applications
- Reduce video resolution in code
- Update graphics drivers

## Technical Details

### Angle Calculation
Uses arctangent to calculate angles between three points (joints):
```
angle = arctan2(c.y - b.y, c.x - b.x) - arctan2(a.y - b.y, a.x - b.x)
```

### Motion Tracking
- Stores last 30 angle measurements
- Detects velocity changes
- Smooths out noise in measurements

### Form Score Calculation
- Starts at 100%
- Deducts points for form violations
- Updates in real-time for each frame

## Future Enhancements

Potential improvements:
- [ ] Add more exercises (lunges, shoulder press, etc.)
- [ ] Voice feedback for form corrections
- [ ] Workout session logging
- [ ] REST API for mobile app integration
- [ ] Multi-person tracking
- [ ] Exercise recommendations based on performance
- [ ] Progress tracking over time
- [ ] Custom workout programs

## License

This project is open source and available for educational purposes.

## Credits

Built using:
- Google MediaPipe for pose estimation
- OpenCV for computer vision
- NumPy for numerical computation

## Support

For issues or questions:
1. Check the troubleshooting section
2. Ensure all dependencies are installed correctly
3. Verify your Python version is 3.8+

---

**Stay fit and track your progress with AI! 💪**
