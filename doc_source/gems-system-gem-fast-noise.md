# Fast Noise Gem<a name="gems-system-gem-fast-noise"></a>


****  

|  | 
| --- |
| This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\.  | 

The **FastNoise Gradient **Gem uses the third\-party, open source [FastNoise](https://github.com/Auburn/FastNoise) library to provide a variety of high\-performance noise generation algorithms in Amazon Lumberyard\. You can use noise generation to generate content in a game\.

The **FastNoise Gradient **Gem provides the [FastNoise Gradient](component-gradients-fastnoise.md) component which expresses noise generation algorithms as **Gradient signals**\. Any system that's compatible with the **Gradient Signal Gem**, such as **Vegetation**, can use noise generation\.

Gradient signals are values that range from 0\.0 to 1\.0 and are automatically mapped to world positions\. They are typically visualized as either greyscale images or waveforms\.

Examples of noise algorithms:

![\[Perlin Noise\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/gems/gems-system-fastnoise-perlin.png)

![\[Cellular Noise.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/gems/gems-system-fastnoise-cellular.png)

![\[White Noise\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/gems/gems-system-fastnoise-white.png)

## Enable the FastNoise Gradient Gem<a name="enable-gem-fastnoise-gradient"></a>

To make the FastNoise Gradient component available in Lumberyard, you must build and configure your project with the FastNoise Gradient Gem enabled\.

**To enable the FastNoise Gradient Gem**

1. Use Project Configurator to add the FastNoise Gradient Gem to your project\. 

1. Configure your project\. Use the following command\.

   ```
   lmbr_waf configure
   ```

1. Build your project\. Use the following command\.

   ```
   lmbr_waf build_win_x64_vs2019_profile -p all --progress
   ```

For more information on Gems, see the [Gems documentation](gems-system-gems.md)\. 