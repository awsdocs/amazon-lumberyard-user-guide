# FastNoise Gradient<a name="component-gradients-fastnoise"></a>

The **FastNoise Gradient** component generates gradient signals with pseudorandom values\. The values are mapped to the world positions in the game project\. It uses the third\-party, open source [FastNoise](https://github.com/Auburn/FastNoise) library, which provides a collection of noise algorithms to generate different noises\. You can interprate the values to produce a variety of game effects throughout the world\. For example, you can use this component with the Vegetation Gem to randomly scatter vegetation throughout your world\. 

The generated gradient signals can be used with other components provided by the **Gradient Signal**  gem\. 

The **FastNoise Gradient** component is provided by the [Fast Noise Gem](gems-system-gem-fast-noise.md)\. 

![\[Properties of the FastNoise Gradient component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component/fastnoise-gradient-component-noisetypes.png)

## Properties<a name="component-gradients-random-noise-properties"></a>

The **FastNoise Gradient** component has the following properties\. The properties listed varies depending on the **Noise Type** property\. 

**Preview and Preview Settings**  
A preview image of the gradient signal\.  

**Noise Type**  
The type of pseudorandom algorithm used to generate noise\.  
+ **Value**: First, this algorithm generates noise in a similar way as the **White Noise** noise type\. Then, each value is interpolated with other surrounding values\. The result looks like a zoomed\-out version of the **White Noise** noise type\. 
+ **Value Fractal**: First, this algorithm generates noise in a similar way as the **Value** noise type\. Then, it creates fractals using those values\. 
+ **Perlin**: The perlin noise algorithm generates noise in a more natural, ordered sequence\. This noise type is well\-suited for modeling natural phenomena such as clouds, water, and vegetation distributions 
+ **Perlin Fractal**: First, this algorithm generates noise in a similar way as the **Perlin** noise type\. Then, it creates fractals using those values\.
+ **Simplex**: This algorithm generates noise in a similar way as the Perlin noise type, but with less directional artifacts and improved computational complexity\. 
+ **Simplex Fractal**: First, this algorithm generates noise in a similar way as the **Simplex** noise type\. Then, it creates fractals using those values\. 
+ **Cellular**: First, the cellular noise algorithm selects random feature points throughout the world and assigns each a value\. Then, the gradient signals mapped to the world coordinates have the same value as its closest feature point\. The result looks like of clusters of different values\. 
+ **White Noise**: This algorithm generates pseudo\-random values using the world coordinates\. The result produces extremely different values for adjacent world points\. 
+ **Cubic**: First, this algorithm generates noise in a similar way as the **White Noise** noise type\. Then each value is interpolated with other surrounding values using a cubic function\. The result looks similar to the **Perlin** noise type, but with less directional artifacts and a higher occurance of extreme values
+ **Cubic Fractal**: First, this algorithm generates noise in a similar way as the **Cubic** noise type\. Then, it creates fractals using those values\. 

**Random Seed**  
The algorithm uses this value to generate a random number sequence\. Different values generate different sequences\. The slider goes from **1** to **100**, but you can enter any value from **1** to **214748647**\.

**Frequency**  
*A value that scales the generated noise\.* A smaller value zooms into the noise, making the noise appear larger and less frequent\. A larger value zooms out of the noise, making the noise appear smaller and more frequent\.

**Octaves**  
*Fractal noise types only\.* The number of repetitions in the algorithm to generate Fractal noise\. A higher value causes finer details in the noise\. Values greater than 4 are almost unnoticeable\.

**Lacunarity**  
*Fractal noise types only\.* A multiplier that defines how much the frequency changes with each octave\. A smaller value zooms into the noise, making the noise appear larger and less frequent\. A larger value zooms out of the noise, making the noise appear smaller and more frequent\.

**Gain**  
*Fractal noise types only\.* A multiplier that blends between the lower octaves and the higher octaves\. A smaller blends towards the lower octaves, a higher value blends towards the higher octaves\.

**Distance Function**  
*Cellular noise types only\.* The cellular noise algorithm uses the distance function to calculate which cell values to use for a given point in the world\. It affects how the cellular shape is distorted\.

**Return Type**  
*Cellular noise types only\.* The cellular noise calculation returns this value and uses it to generate the gradient signal\.  
+ **Distance2Div** the distance of the closest feature point divided by the distance of the second\-closest feature point\.
+ **Distance** the distance to the nearest feature point at any given world position\.
+ **Distance2** the distance to the second\-nearest feature point at any world position\.
+ **Distance2Add** the distance of the two closest feature points added together\.
+ **Distance2Mul** the distance of the two closest feature points multiplied together\.
+ **Distance2Sub** the distance of the two closest feature points subtracted together\.
+ **CellValue** the value of the nearest feature point at any given world position\.

**Jitter**  
*Cellular noise types only\.* A value that scales the location of the feature points\. For ideal results, use a value between **0\.0** and **1\.0**, where **0\.0** provides no jitter\. 

### Advanced Settings<a name="component-gradients-random-noise-advanced-properties"></a>

In addition, the **FastNoise Gradient** component has the following advanced properties: 

![\[Advanced properties of the FastNoise Gradient component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component/gradient/random-noise-gradient-properties.png)

**Interpolation**  
*Value, Value Fractal, Perlin, and Perlin Fractal noise only\.* The noise generation alrogithm uses this type of interpolation when calculating noise values\.  
+ **Linear** interpolation provides angular artifacts\.
+ **Hermite** interpolation provides smoothed, blurred noise\.
+ **Quintic** interpolation is similar to hermite, but provides more defined edges without calculating angular artifacts\.

**Fractal Type**  
*Fractal noise types only\.* The noise generation algorithm uses this type of fractal when calculating the noise values\.  
+ **FBM \(Fractional Brownian Motion\)** adds multiples of frequencies and amplitudes of the noise signal together\.
+ **Billow** is a variant of FBM where the absolute value of multiple frequencies and amplitudes are added toegther\. This produces extreme gradient signal values\.
+ **Rigid Multi** is also a variant of FBM, where the inverse of the absolute value of multiple frequencies and values of the noise signal are subtracted from each other\. This produces extreme elevations in the gradient signal values\.