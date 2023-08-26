# yolov8-crowded-images

These images are dedicated to helping your Yolo model improve at detecting basic objects in large crowds. These images are not perfect, and if you do not intend to use Yolo for crowded or busy images, I don't know how it will respond.

The classes included in this repository are:

nc: 8
names: [Car, "Truck", "Person", "Bicycle", "Motorcycle", "Bus", "Group_of_People", Group_of_Cars]

You can put this in your YAML file when training. The order does matter; otherwise, it will detect classes as other classes.

These images can contain anywhere from a couple dozen annotations to a few hundred. (Per image). With this, you would be adding two classes to Yolo: "Group_of_People" and "Group_of_Cars". If you want to continue to train using these terms, I have generalized the way that I have annotated either of these below, along with descriptions of how I marked all other classes if you want to align yours with mine. It is easy but time-consuming to do.

Car: Any distinguishable car in the image that is not completely blocked by lights. If you can see it, you should mark it. Cabs, vans—if it isn't a bus or truck, it's a car.

"Truck" , "Bicycle" , Motorcycle," and Bus: Same as cars, except, you know, it's whatever else it is.

(A note for motorcycles.) I have not added, as of right now, Group_of_Motorcycles, as those can be found really only in places like Vietnam and Camobodia, but if you will be utilizing images from those areas, I highly suggest you add it.

Person: Any distinguishable person. If you can see them and they aren't almost fully hidden by an object, mark them. If you can only see the face, just mark the face. If you can see portions of the body, mark the entire body.

Group_of_...: As a person, you should be able to tell that it is a large group of that object; however, they are not distancing from one another. It is just quite a large lump. It is a lot more than just common sense. These are normally much further from the start of the shot; you can refer to the images to see the situations where they are applicable and where they aren't.

There are a lot of things to note when using these images in your training. First and foremost, no credit or attribution is required in any way, but if you want to, it could help others find the resource. Secondly, if you intend to video-analyze simple images, this is not a good idea. I've had to train my model 24 hours a day for weeks on lots of different images to make sure it doesn't think the sides of buildings are cars—all that to say, unless you will be processing busy images with lots of objects to detect. This is really only for a specific group of people with a specific task. If you do need them, extensive monitoring and training are required over a decent period of time to make sure that it completely learns. It is very difficult to get consistent reads on blurry objects or objects far away from the shot.

If you need a guide on how to use these to train your model, I will explain below. Otherwise, you are free to use and contribute! Make sure that if you contribute, you contribute images that align with those that have already been added.

To use these, I am going to assume that you have a working YoloV8 model in Python. If you don't, it's super, super simple. Just read their GitHub: https://github.com/ultralytics/ultralytics
Once y
Once you have that, you need to create a config.yaml. It doesn't need to be called config; I am really unsure of what the official name for it is, but it does need to be a.yaml. Then you need to import the images and annotations folder(s) that you wish to train on. Once you've got all that, it's time to start training. Your YAML should look something like this at the most basic level:

#roots
train: "Path/To/Training/Images"
val: "Path/To/Val/Images"

# Classes
nc: 8
names:
  [
    "Car",
    "Truck",
    "Person",
    "Bicycle",
    "Motorcycle",
    "Bus",
    "Group_of_People",
    "Group_of_Cars",
  ]

Your Python and Yolo codes are based on personal preference. If you have that all setup, alongside all the dependencies (which, if you don't have any, when you try to run it, it will tell you what you need), you are good to go! Just start training. Please note that Yolo suggests that the ideal number of epochs is 34. Especially with much smaller but much more detailed datasets such as these, you want to make sure that you do a good amount of epochs to make it efficient. You should run training (after it finishes with x epochs) at least two more times; I would say go until you see no changes in your F1 curve. Then you can add some new images to the dataset and test again, or add a whole other dataset.

That's it! Easy, simple. Thanks to Yolo, anyone can really do this!
