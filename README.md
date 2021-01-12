  Copy-to-point-Maya
======
Script to generate and copy structure with differents parameters. Made with Python 3. Maya Autodesk.

## Requirement
* Maya 2020 from Autodesk of course :)
* Nothings else

## Setup
  In Maya you have a script editor for MEL and Python.
   
  More help can be find for the script interface in Maya 2020 : http://help.autodesk.com/view/MAYAUL/2020/ENU/?guid=GUID-7C861047-C7E0-4780-ACB5-752CD22AB02E
  
  Now, you just have to copy the content from main.py or take it just below and past it in the Python script editor.
  
```
$ 
import maya.cmds as mc
import random as r

        
#------------------------------------------------------------------------------
# GET ALL POINTS
#------------------------------------------------------------------------------

def getAllPoints():
    """
    GET ALL POINTS :
        Takes the position of each point of the selected object and saves it in a list.
    """
    
    target = mc.ls(sl=True, dag = True, type="mesh", ni = True)
    xformPos = mc.xform(target[0] + ".vtx[*]", q=True, t=True, ws=True)
    vtxWorldPos = zip(xformPos[0::3],xformPos[1::3],xformPos[2::3])
    
    return vtxWorldPos

    
#------------------------------------------------------------------------------
# GET PIVOT
#------------------------------------------------------------------------------
    
def setPivotCube():
    """
    SET PIVOT CUBE :
        Places the pivot point of the object "Cube" at its lowest pole.
    """
    mc.xform(piv=[0, scaleOfObject*-.5, 0])
    mc.move(0, scaleOfObject*.5, 0)
    mc.makeIdentity(apply=True, t=True)
    
def setPivotSphere():
    """
    SET PIVOT SPHERE :
        Places the pivot point of the object "Sphere" at its lowest pole.
    """
    mc.xform(piv=[0, (scaleOfObject*2)*-.5, 0])
    mc.move(0, (scaleOfObject*2)*.5, 0)
    mc.makeIdentity(apply=True, t=True)

def setPivotCone():
    """
    SET PIVOT CONE :
        Places the pivot point of the object "Cone" at its lowest pole.
    """
    mc.xform(piv=[0, scaleOfObject*-.5, 0])
    mc.move(0, scaleOfObject*.5, 0)
    mc.makeIdentity(apply=True, t=True)

#------------------------------------------------------------------------------
# GET ALL COLOR POINTS
#------------------------------------------------------------------------------

def getAllColorPoints():
    """
    GET ALL Color POINTS :
        Takes the color of each point of the selected object and saves it in a list.
    """
    
    mc.select(target)
    getColorVtx = mc.polyColorPerVertex(query = True, r = True, g = True, b=True, cdo = True)
    vtxWorldColor = zip(xformColor[0::3],xformColor[1::3],xformColor[2::3])
    
    return vtxWorldColor
    
    
#------------------------------------------------------------------------------
# RANDOMIZE COLOR
#------------------------------------------------------------------------------

def getAllColorPoints():
    if setColorObject == True :
        vtxColor = getAllColorPoints()
        
        mc.select(source)
        mc.polyColorPerVertex(query = True, r = , g = True, b=True, cdo = True)
        
        



#------------------------------------------------------------------------------
# RANDOMIZE ROTATION
#------------------------------------------------------------------------------
    
def randomizeObjectRotation(minRandRotate, maxRandRotate):
    """
    RANDOMIZE OBJECT ROTATION :
        Randomizes the rotation of an object between a minimum and a maximum. 
    """
    if minRandRotate != 0 and maxRandRotate != 0:
        randomizedRotate = r.randrange(minRandRotate, maxRandRotate+1)
        mc.rotate(0, randomizedRotate, 0)


#------------------------------------------------------------------------------
# RANDOMIZE SCALE
#------------------------------------------------------------------------------
       
def randomizeObjectScale(minRandScale, maxRandScale):
    """
    RANDOMIZE OBJECT SCALE :
        Randomizes the scale of an object between a minimum and a maximum. 
    """
    if setUniformeScale == True:
        if minRandScale != 1 or maxRandScale != 1:
            randomizedScale = r.randrange(minRandScale, maxRandScale+1)
            mc.scale(randomizedScale, randomizedScale, randomizedScale)
            
    else:
        if minRandScale != 1 or maxRandScale != 1:
            randomizedScaleX = r.randrange(minRandScale, maxRandScale+1)
            randomizedScaleY = r.randrange(minRandScale, maxRandScale+1)
            randomizedScaleZ = r.randrange(minRandScale, maxRandScale+1)
            mc.scale(randomizedScaleX, randomizedScaleY, randomizedScaleZ)

     
#------------------------------------------------------------------------------
# GENERATE OBJECT BY CYCLE OR BY RANDOM
#------------------------------------------------------------------------------

# CYCLE ---------------------
    
def generateObjectByCycle():
    """
    GENERATE OBJECT BY CYCLE :
        Generates the objects "Cube", "Sphere" and "Cone" in this order on the points of the selection.
    """
    source = []
    vtxPos = getAllPoints()
    i = 1
    scaleOfObject = 1
    for x in vtxPos:
        if i==1:
            mc.polyCube(h=scaleOfObject)
            setPivotCube()
            randomizeObjectRotation(minRandRotate, maxRandRotate)
            randomizeObjectScale(minRandScale, maxRandScale)
            source.append()    
                
        elif i==2:
            mc.polySphere(r=scaleOfObject)
            setPivotSphere()
            randomizeObjectRotation(minRandRotate, maxRandRotate)
            randomizeObjectScale(minRandScale, maxRandScale)
            source.append()
                
        elif i==3:
            mc.polyCone(h=scaleOfObject)
            setPivotCone()
            randomizeObjectRotation(minRandRotate, maxRandRotate)
            randomizeObjectScale(minRandScale, maxRandScale)
            source.append()
            
        mc.move(x[0],x[1],x[2],a=True)        
        i=i+1
        total = i
            
        if i==4:
            i=1
        
                

# RANDOM ---------------------            
                            
def generateObjectByRandom():
    """
    GENERATE OBJECT BY RANDOM :
        Generates randomly the objects "Cube", "Sphere" and "Cone" on the points of the selection.
    """
    source = []
    vtxPos = getAllPoints()
    for x in vtxPos:    
        randomozedObject = r.randrange(3)
        if randomozedObject == 0:
            mc.polyCube(h=scaleOfObject)
            setPivotCube()    
            randomizeObjectRotation(minRandRotate, maxRandRotate)
            randomizeObjectScale(minRandScale, maxRandScale)
            source.append()
        
        elif randomozedObject == 1:
            mc.polySphere(r=scaleOfObject)
            setPivotSphere()
            randomizeObjectRotation(minRandRotate, maxRandRotate)
            randomizeObjectScale(minRandScale, maxRandScale)
            source.append()
            
        
        elif randomozedObject == 2:
            mc.polyCone(h=scaleOfObject)
            setPivotCone()
            randomizeObjectRotation(minRandRotate, maxRandRotate)
            randomizeObjectScale(minRandScale, maxRandScale)
            source.append()
            
        
        mc.move(x[0],x[1],x[2],a=True)
            


#------------------------------------------------------------------------------
# ASSEMBLE INTO A FUNCTION
#------------------------------------------------------------------------------

def copy2Points(cycle=True, randrotate = [], randscale = [], useuniformscale=True):
    """
    COPY TO POINTS :
        Generates objects "Cube", "Sphere" and "Cone" on the points of the selection.
        These objects can be modified and influenced by several parameters.
        
            CYCLE : (Boolean)
            |    if it's True : objects will be generated in the following order: "Cube", "Sphere", "Cone".
            |    if it's False : objects will be randomly generated.
                
            
            RANDROTATE : [minRandRotate, maxRandRotate]
            |    Randomizes the rotation of an object between a minimum (minRandRotate) and a maximum (maxRandRotate).
            |    FOR DEFAULT SETTINGS : randrotate = [0,0]
            |    
            |    minRandRotate :
            |        TYPE : int
            |        DEFINITION : minimum rotation value of an object. 
            |        
            |     maxRandRotate : 
            |        TYPE : int
            |        DEFINITION : maximum rotation value of an object.
 
            
            RANDSCALE : [minRandScale, maxRandScale]
            |    Randomizes the scale of an object between a minimum (minRandScale) and a maximum (maxRandScale).
            |    FOR DEFAULT SETTINGS : randscale = [1,1]
            |    
            |    minRandScale :
            |        TYPE : int
            |        DEFINITION : minimum scale value of an object. 
            |        
            |     maxRandScale : 
            |        TYPE : int
            |        DEFINITION : maximum scale value of an object.
            

            USEUNIFORMESCALE : (Boolean)
            |    if it's True : object will have the same scale value in x, y and z.
            |    if it's False : object will have different scale values in x, y and z. For this to work, you must also put a different min and max number in the variable "randomscale".
            
    """
    global minRandRotate, maxRandRotate
    minRandRotate = randrotate[0]
    maxRandRotate = randrotate[1]
    
    global minRandScale, maxRandScale
    minRandScale = randscale[0]
    maxRandScale = randscale[1]
    
    global setUniformeScale
    setUniformeScale = useuniformscale
    
    global setColorObject
    setColorObject = useColor
    
    # Fonction Cycle or Random -------------------
    if cycle == True:
        generateObjectByCycle()
            
    elif cycle==False:
        generateObjectByRandom()
    

           
#------------------------------------------------------------------------------
# COPY TO POINTS FUNCTION
#------------------------------------------------------------------------------    

copy2Points(cycle=False, randrotate=[1, 2], randscale =[1, 1], useuniformscale=False)

#copy2Points(source, target, randrotate=(), randscale=(), useuniformscale=True, cycle=False, packinstance=True, useColor=True, seed=12345)

$ 
```
  
## How to use it

  In Maya, you can't really make a good architecure of code for your project. Beacause scripting is definitely not the most interresting part in Maya.
  
  Setup you grid as you want and select it before launch the script.
  
  So there is a call to a function named **"copy2Points()"** with differents parameters. That where you can set as you want the integer and bool value.
  
  **For the moment only the "cycle / randrotate / randscale / useuniformscale" function is available. More function will came soon.**
  
## In the future
  
  Here is the kind of function that will be use to the script. For the moment only "cycle / randrotate / randscale / useuniformscale" is available.
  
```
$ 
copy2Points(source, target, randrotate=(), randscale=(), useuniformscale=True, cycle=False, packinstance=True, useColor=True, seed=12345)
$ 
```
  
## Version 
* Version 0.19

## Contact
#### Developer
* e-mail: nvel.clainche@gmail.com

