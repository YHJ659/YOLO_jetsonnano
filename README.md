# Camera를 이용한 YOLO
<https://github.com/jetsonmom/yoloV8_jetson4GB?tab=readme-ov-file>

위 링크의 설명에 따라 아나콘다와 yolo v8 설치 및 환경 설정한다.

yolo 실행을 위해서는 line88 def predict 코드를 수정해야 한다.

코드 불러오기는 아래 명령어

```
gedit  detectY8.py
```

```
def predict(cfg=DEFAULT_CFG, use_python=False):
   
    brtsp = True
	
    if brtsp: 
		#cfg.source ='https://www.youtube.com/watch?v=yTIQMnnaBZo'
        cfg.source ='rtsp://admin:satech1234@192.168.0.151:554/udp/av0_0'
       
    else:
        cfg.source = '/home/dli/Jetson-Nano2/V8'
        
    cfg.imgsz = 640
    cfg.show    = True    
    cfg.iou     = 0.45
    cfg.conf    = 0.15
    cfg.data    = "coco128_kor.yaml"
    cfg.model   = 'yolov8n.pt'

    source = cfg.source if cfg.source is not None else ROOT / 'assets' if (ROOT / 'assets').exists() \
        else 'https://ultralytics.com/images/bus.jpg'

    args = dict(model=cfg.model, source=source)
    if use_python:
        from ultralytics import YOLO
        YOLO(cfg.model)(**args)(cfg)
    else:
        predictor = DetectionPredictor(overrides=args)
        predictor.predict_cli()
```

brtsp = True 를 False 로 수정이후에 실행한다.

```
(yolo) yolo@yolo-desktop:~/Jetson-Nano2/V8$ python detectY8.py
```

---

# 실행

![Screenshot from 2024-10-24 19-00-17](https://github.com/user-attachments/assets/ed5e8708-2f9a-47ec-b3f8-fc5aff0b150e)

# 동영상을 이용한 YOLO

```
def predict(cfg=DEFAULT_CFG, use_python=False):
   
    brtsp = False
	
    if brtsp: 
		#cfg.source ='https://www.youtube.com/watch?v=yTIQMnnaBZo'
        cfg.source ='rtsp://admin:satech1234@192.168.0.151:554/udp/av0_0'
       
    else:
        cfg.source = '/home/dli/Jetson-Nano2/V8/output_video.mp4'
        
    cfg.imgsz = 640
    cfg.show    = True    
    cfg.iou     = 0.45
    cfg.conf    = 0.15
    cfg.data    = "coco128_kor.yaml"
    cfg.model   = 'yolov8n.pt'

    source = cfg.source if cfg.source is not None else ROOT / 'assets' if (ROOT / 'assets').exists() \
        else 'https://ultralytics.com/images/bus.jpg'

    args = dict(model=cfg.model, source=source)
    if use_python:
        from ultralytics import YOLO
        YOLO(cfg.model)(**args)(cfg)
    else:
        predictor = DetectionPredictor(overrides=args)
        predictor.predict_cli()
```

위 코드에서 

cfg.source = 0 을 '/home/dli/Jetson-Nano2/V8/output_video.mp4' 로 수정한다.

#실행

![Screenshot from 2024-10-24 19-12-30](https://github.com/user-attachments/assets/93c0b675-c231-42ff-8c41-76b95f8ad3d6)





