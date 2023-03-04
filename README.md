import mediapipe as mp
import cv2

handModel=mp.solutions.hands
handModelDrawing=mp.solutions.drawing_utils
webcam=cv2.VideoCapture(0)

with handModel.Hands(min_detection_confidence=0.5,min_tracking_confidence=0.5) as hands:
    while True:
        control,frame=webcam.read()
        rgb=cv2.cvtColor(frame,cv2.COLOR_BGR2RGB)
        result=hands.process(rgb)
        if result.multi_hand_landmarks:
            for handLandmark in result.multi_hand_landmarks:
                handModelDrawing.draw_landmarks(frame,handLandmark,handModel.HAND_CONNECTIONS)
        cv2.imshow("Hands",frame)
        if cv2.waitKey(10)==27:
            break
            
            ![Screenshot_112](https://user-images.githubusercontent.com/59823440/222881164-58a8cc82-a2ae-42be-93be-bd4f9b0351bd.png)


 
import cv2
import mediapipe as mp

webcam=cv2.VideoCapture(0)
mp_face=mp.solutions.face_mesh
mp_drawing=mp.solutions.drawing_utils
with mp_face.FaceMesh(min_detection_confidence=0.5,min_tracking_confidence=0.5) as face_mesh:
    while True:
        control,frame=webcam.read()
        if control==False:
            break
        rgb=cv2.cvtColor(frame,cv2.COLOR_BGR2RGB)
        result=face_mesh.process(rgb)
        if result.multi_face_landmarks:
            for face_landmarks in result.multi_face_landmarks:
                mp_drawing.draw_landmarks(frame,face_landmarks,mp_face.FACEMESH_TESSELATION)
        cv2.imshow("Test",frame)
        if cv2.waitKey(10)==27:
            break
            
            
            ![Screenshot_113](https://user-images.githubusercontent.com/59823440/222881171-57f788af-f5db-48a6-a616-b3a6c18c2de2.png)
