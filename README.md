# yolov8-crowded-images

These images are dedicated to help your Yolo model improve at detecting basic objects in large crowds. These images are not perfect, and if you do not intend to use Yolo for crowded or busy images, I don't know how it will respond.

The classes included in this repository are: 

nc: 8
names: [ "Car", "Truck", "Person", "Bicycle", "Motorcycle", "Bus", "Group_of_People", "Group_of_Cars" ]

You can put this in your .yaml file when training. The order does matter, otherwise it will detect classes as other classes. 

These images can contain anywhere from a couple dozen annotations or a few hundred. (Per image). With this, you would be adding two classes to Yolo, "Group_of_People" & "Group_of_Cars". If you want to continue to train using these terms, I have generalized the way that I have annotated either of these below, alongisde descriptions of how I marked all other classes if you want to align yours with mine. It is deasy but time consuming to do. 

"Car" : Any distingushable Car in the image that is not completley blocked by lights. If you can see, you should mark it. Cabs, Vans - if it isn't a bus or truck, it's a car. 

"Truck" , "Bicycle" , "Motorcycle" , "Bus"  : Same as car, except, you know, it's whatever else it is.

(A note for motorcycles. I have not added, as of right now, Group_of_Motorcycles, as those can be found really only in places like Vietnam and Camobodia, but if you will be utilizing images from those areas I highly suggest you add it)

"Person" : Any distingushable person. If you can see them, and they arent almost fully hidden by an object, mark them. If you can only see the face, just mark the face. If you can see portions of the body, mark the entire body. 

"Group_of_..." : As a person, you should be able to tell that it is a large group of that object, however, they are not distingushable from one another. It is just quite a large lump. It is a lot more of just common sense. Theese are normally much further from the start of the shot, you can refer to the images to see the situations where they are applicable and they aren't. 

There are a lot of things to note when using these images in your training. First and foremost, no credit or attribution is required in anyway, but if you want to, it could help others find the resource. Secondly, if you intend to video anayzling or simple images, this is not a good idea. I've had to train my model 24 hours a day for weeks on lots of different images to make sure it doesn't think the side of buildings are cars - all that to say, unless you will be processing busy images with lots of objects to detect. This is really only for a specific group of people with a specific task. If you do need them, extensive monitoring and training is required over a decent period of time to make sure that it completley learns. It is very difficult to get consitent reads on blurry objects, or objects far away from the shot. 

If you need a guide on how to use these to train your model, I will explain below. Otherwise, you are free to use and contribute! Make sure if you contribute you contribute images that align with those that have already been added. 

To use these, I am going to assume that you have a working yoloV8 model in python. If you don't, it's super super simple. Just read their github: https://github.com/ultralytics/ultralytics
Once y
Once you got that, you need to create a config.yaml. It doesn't need to be called config - I am really unsure of what the professinal name for it is, but it does need to be a .yaml. Then you need to import the images & annotations folder(s) that you wish to train on. Once you've got all that, it's time to start training. Your .yaml should look something like this at the most basic level:

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

Your python & Yolo code are based on personal preference. If you have that all setup, alongside all the dependicies (Which, if you don't have, when you try to run it, it will tell you what you need), you are good to go! Just start training. Please note that yolo suggests that the ideal number of epochs is 34 - Especially with much smaller, but much more detailed datasets such as these, you want to make sure that you do a good amount of epochs to make it efficient. You should run training (after it finishes with x epochs) at least two more times - I would say go until you see no changes in your F1 Curve. Then you can add some new images to the dataset and test again, or add a whole other dataset. 

That's it! Easy, simple, thanks to Yolo anyone can really do this! 
