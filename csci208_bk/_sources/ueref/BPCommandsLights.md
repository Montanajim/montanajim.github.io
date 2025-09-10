## Blueprint Commands to Manipulate Lights in Unreal Engine

Unreal Engine provides a variety of blueprint nodes to control the behavior of lights, including their intensity, color, and direction. Here are some common examples:

### Intensity and Color

- **Set Light Intensity:** Sets the overall intensity of a light.
- **Set Light Color:** Sets the color of a light.
- **Set Light Temperature:** Sets the temperature of a light (for example, to create a warmer or cooler tone).
- **Set Light Flicker:** Enables or disables flicker effects for a light.

### Direction and Rotation

- **Set Directional Light Rotation:** Sets the rotation of a directional light.
- **Set SpotLight Inner Cone Angle:** Sets the inner cone angle of a spotlight.
- **Set SpotLight Outer Cone Angle:** Sets the outer cone angle of a spotlight.
- **Set PointLight Attenuation Radius:** Sets the attenuation radius of a point light.

### Shadows

- **Set Light Cast Shadows:** Enables or disables shadow casting for a light.
- **Set Light Shadow Bias:** Adjusts the shadow bias to reduce shadow artifacts.
- **Set Light Shadow Resolution:** Sets the resolution of the shadow map.

### Other Properties

- **Set Light Mobility:** Sets the mobility of a light (static, movable, or dynamic).
- **Set Light Cast Dynamic Shadows:** Enables or disables dynamic shadow casting for a light.
- **Set Light Volumetric Intensity:** Sets the intensity of volumetric lighting effects.

### Example: Creating a Pulsating Light

1. **Create a new blueprint class** based on a light actor (e.g., PointLight).
1. **Add a Timer node** to the Event Graph.
1. In the Timer's Tick event:
   - Get the current intensity of the light.
   - Calculate a new intensity based on a sine wave function.
   - Set the light's intensity to the new value.

**Remember:** The specific nodes and their usage can vary depending on the type of light you're working with (point light, spotlight, directional light) and the desired effects. Experiment with different combinations to achieve the desired results.