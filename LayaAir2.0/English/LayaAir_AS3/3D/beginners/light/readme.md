##LayaAir3D Light Source

Lighting is very important in the 3D world. Three-dimensional objects can produce three-dimensional light and shadow changes, color tone changes, projection and so on, which can be used for lighting settings.

##Lighting type

There are many kinds of lights. Different light sources have different effects and can set different parameters. In the 3D project created by IDE, we can modify the code to see different kinds of lighting effects.

###Point Light

Spotlight is a source of light that emits light in all directions, also known as omnidirectional light or spherical light. In reality, point light sources, such as bulbs and candles, can feel that point light sources have attributes of intensity, color and attenuation radius.


```java

	//创建点光
	var light:PointLight = scene.addChild(new PointLight()) as PointLight;
	//移动灯光位置
	light.transform.translate(new Vector3(-3,5,0));
	//设置点光照亮范围
	light.range=6;
```

Range is the range of the point light source, which is equivalent to the illumination range of the point light. The larger the value, the larger the illumination range. Because the illumination range in Fig. 1 is small, the area not illuminated is black. In Fig. 2, the illumination range exceeds the distance between the light and the model, so it is illuminated completely.





  ![图片2](img/2.png)(Fig. 1)




###Direction Light

Parallel light is quite different from point light. It has a fixed direction, can be set by radian value, and has no attenuation and illumination range. It will illuminate all models in the whole scene. In the 3D world, it is often used to simulate sunlight in a fixed direction.


```java

	//创建平行光
	var light:DirectionLight = scene.addChild(new DirectionLight()) as DirectionLight;
	//设置平行光方向
	light2.transform.worldMatrix.setForward(new Vector3(0, -1.0, 0));
```


The direction of setForward parallel light represents the direction of x, y and Z axes respectively. Negative axes are negative axes, positive axes are positive axes. The range of values is -1-0-1. Beginners can set values to observe the direction change in this range.



###Spotlight

Focusing light refers to light emitted from a specific light source direction, such as flashlight, stage lamp, etc. The illumination area is enlarged gradually according to the distance factor, and the edge of the illumination area is also attenuated.

```java

	//添加聚光
	var light:SpotLight=scene.addChild(new SpotLight()) as SpotLight;
	//设置聚光的位置
	light.transform.position=new Vector3(0,5,0)
	//设置聚光的方向
	light3.transform.worldMatrix.setForward(new Vector3(0,-1,0));
	//设置聚光范围
	light.range=5;
	//设置聚光锥形角度
	light3.spotAngle = 50;
```


Attachment is the attenuation of the spotlight. The smaller the value is, the smaller the blur of the spotlight aperture is, and vice versa.

Direction is the direction of focusing light, and the value of direction is set in the same way as that of parallel light.

Range is the irradiation range of focused light, which is similar to point light. The difference is that focus light has direction, but point light has no direction.

![图片3](img/3.png)(Fig. 2)![图片4](img/4.png)(Fig. 3)



##Photochromic elements

When lighting is used in the scene, all 3D models in the light range will have an impact. The lighting in the LayaAir 3D engine includes the following elements, which are used to adjust the brightness and color of the scene.

###Ambient color

**Tips: After version 1.7.9 of the engine, the ambient color settings of the lights have been cancelled, and the old version can be used as usual. The environment color can be set in the material.**

Ambient color can easily understand the atmosphere color of the scene. For the models in the scene, their bright and dark sides will be affected by the environmental color at the same time. The brighter the environmental color, the higher the overall brightness of the model. Of course, environmental color is also often used in tone processing. It can adjust the atmosphere of red, orange, yellow, green, blue and purple through environmental tone.

The code sets the ambient color as follows, which produces yellow ambient light, and the model is covered with a layer of yellow (Figure 4).

In the previous course, we introduced that three-dimensional vectors can be used to set color values. Let's review again that three elements in vectors represent red, green and blue colors respectively. They are combined into a variety of colors. The maximum value of each color is 1, which will produce an exposure effect when exceeded.


```java

//设置灯光的环境色为纯黄色（计算机中，红+绿=黄）
light.ambientColor = new Vector3(1,1,0);
```


![图片5](img/5.png)(Fig. 4)



###Diffuse color

**Tips: After version 1.7.9 of the engine, the color light color attribute settings have been added, which works the same as diffuseColor.**

Also known as light source color, is the light on the model affected by the brightness and color of the light surface, such as simulated candle light, can adjust the light source color yellow, then the model will be added yellow hue by the light surface.

In the following code, if we set the light source color to pure red, then the model will be affected by the part of illumination, because we set the ambient light (material ambient light or old version ambient light) to yellow, so the light receiving surface is red + yellow = orange color mixture (Fig. 5).


```java

//设置灯光的漫反射色为纯红色
//light.diffuseColor = new Vector3(1,0,0);
//设置灯光颜色为纯红色(与diffuseColor作用相同)
light.color = new Vector3(1,0,0);
```


![图片6](img/6.png)(Fig. 5)

Turning off the ambient light, we can see the effect (Fig. 6), because without the influence of the Yellow ambient color, the light-affected surface of the model becomes the light source color. Therefore, in the process of project development, we have to take into account the mixed effects of light and color attributes.

![图片7](img/7.png)(Fig. 6)



###Specular Color

**Tips: After version 1.7.9 of the engine, the highlight color settings of the lights have been cancelled, and the old version can be used as usual. The highlight color can be set in the material.**

For the model, high light will be generated in the direction of the light source and the angle is sharp and smooth. The brightness and color of high light can be adjusted by the high light color of the light. The default high light color is pure white.

There are two ways to adjust the specular color of the model. One is to set the specular color on the light, and the other is to set the specular map on the material. In most cases, the specular color is adjusted directly on the material, which is more convenient and more realistic.

Because the box model can not produce highlights, we use a smoother sphere model to observe, Figure 7-1 for the code does not set highlights color, the engine default value is pure white, thus showing a white dimming. In the following code, we set the highlight color to blue. Figure 7-2 shows clearly that the sphere produces a blue highlight because it is purple when added to the diffuse reflection red.


```java

//修改材质的高光颜色
 material.specularColor = new Vector4(0.5,0.5,1);
```


![图片8-1](img/8-1.png)(Fig. 7-1)![图片8-2](img/8-2.png)(Fig. 7-2)



###Shadow

Projection is the instant shadows produced when the model is illuminated by light, which can change with the change of light angle, light intensity and model position. Projection is one of the most important factors in the 3D world, which can produce a stronger stereo sense.

Immediate shadows are very performance-degrading and can not be used too much, especially in game scenes. There are a large number of models. Generally, we do not use instant projection, but use static light mapping.

To generate projection in a scene, we need to understand the following attributes of light:

**Shadow:**Whether to turn on the projection, Boolean value, set to true, will take effect.

**Shadow Distance:**The range of projection is the distance from the camera to the model in meters. Models larger than this range will not accept projections and generate projections, and developers can set them according to the size of the scene.

**ShadowPSSMCount:**The higher the number of shadow maps produced, the finer the shadows and the greater the performance loss.

**Shadow Resolution:**The quality of projection, the shadow size in the projection range. By setting the quality of the numerical value, the larger the numerical value, the higher the projection quality and the higher the performance loss. The projection quality value is set in units of N power of 2. By default, it is 512. It can be set to 1024, 2048, etc.

**Shadow PCFType:**Shadow blur level 0-3, the greater the blur value, the softer the shadow, the better the effect, but the more performance consumption.



It is not enough to only turn on and set the attributes of the lighting, but also to modify the projection attributes on the model.

**Recive Shadow:**Whether to accept projection or not, when this attribute of the model is true, the calculated projection will be displayed on the model. In the game, we can set the ground of the scene and the castShadow attribute of the model in the movable area of the scene to true.

**CastShadow:**Whether projection occurs or not, when the model attribute is true, the light projection is calculated according to the position of the model, the shape and size of the model mesh, and the angle of the light, and then the projection is generated on the model receiving the shadow. Active game elements such as characters in the scene, NPC, etc. can open this property.

In order to understand projection well, we use parallel light in the following sample code, and create box box box model and sphere model to load into the scene. Sphere is used to generate shadows and receive projection on the box.


```java

package {
	
	import laya.d3.core.BaseCamera;
	import laya.d3.core.Camera;
	import laya.d3.core.MeshSprite3D;
	import laya.d3.core.Sprite3D;
	import laya.d3.core.light.DirectionLight;
	import laya.d3.core.material.StandardMaterial;
	import laya.d3.core.scene.Scene;
	import laya.d3.math.Vector3;
	import laya.d3.math.Vector4;
	import laya.d3.resource.Texture2D;
	import laya.d3.resource.models.BoxMesh;
	import laya.d3.resource.models.SphereMesh;
	import laya.display.Stage;
	import laya.utils.Stat;

	public class LayaAir3D 
    {
		public function LayaAir3D()
        {
			//初始化引擎
			Laya3D.init(1000, 500,true);
			
			//适配模式
			Laya.stage.scaleMode = Stage.SCALE_FULL;
			Laya.stage.screenMode = Stage.SCREEN_NONE;

			//开启统计信息
			Stat.show();
			
			//添加3D场景
			var scene:Scene3D = Laya.stage.addChild(new Scene3D()) as Scene3D;
			 
			//创建摄像机(横纵比，近距裁剪，远距裁剪)
			var camera:Camera = new Camera( 0, 0.1, 100);
			//加载到场景
			scene.addChild(camera);
			//移动摄像机位置
			camera.transform.translate(new Vector3(0, 4, 8));
			//旋转摄像机角度
			camera.transform.rotate(new Vector3( -30, 0, 0), true, false);
			
			//创建方向光
		    var light:DirectionLight = scene.addChild(new DirectionLight()) as DirectionLight;
		    //移动灯光位置
		    light.transform.translate(new Vector3(0,5,0));
			//设置灯光方向
		    light.transform.worldMatrix.setForward(new Vector3(0.3,-1, 0));
			//设置灯光漫反射颜色
			light.diffuseColor = new Vector3(1, 0, 0);
          
          	//设置灯光环境色
//		    scene.ambientColor = new Vector3(1, 1, 0); 
		 
		    //添加灯光投影
		    light.shadow=true;
			//产生投影的范围（如过小将不会产生投影）
		    light.shadowDistance=45;
          	//生成阴影贴图数量
			light.shadowPSSMCount = 1;
			//模糊等级,越大越高,效果更好，更耗性能
          	light.shadowPCFType=1;
			//投影质量
		    light.shadowResolution=2048;

			 
			//创建盒子模型
			var box:MeshSprite3D = scene.addChild(new MeshSprite3D(new BoxMesh(1.5,1.5,1.5))) as MeshSprite3D;
			//自身y座标旋转
			box.transform.rotate(new Vector3(0,45,0),true,false);
			//接收阴影
			box.meshRenderer.receiveShadow=true;
			
			//创建球体模型
			var sphere:MeshSprite3D = scene.addChild(new MeshSprite3D(new SphereMesh())) as MeshSprite3D;
			//按父空间移动球体
			sphere.transform.translate(new Vector3(0,1.5,0),false);
			//产生阴影
			sphere.meshRenderer.castShadow=true;
			//创建材质
			var material:PBRSpecularMaterial = new PBRSpecularMaterial();
			//材质加载漫反射贴图
		Texture2D.load("h5/res/layabox.png",Handler.create(this,function(text:Texture2D):void{
          material.albedoTexture = text;
          //为模型赋材质（单个材质可赋给多个模型）
          sphere.meshRenderer.material = material;
          box.meshRenderer.material = material;
       	 }));
		}		
	}
}
```




![图片9](img/9.png)(Fig. 8)![图片10](img/10.png)(Fig. 9)

The above two pictures are the effect before and after opening projection. Note that the related attributes described above need to be set on both the lighting and the model. No shadows can be produced without any links.

