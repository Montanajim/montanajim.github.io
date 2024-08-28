# Fire Flicker

## Viewport items created

* Point light - this is the light that lights the fire
  * Place this over a fire asset
* Fire Sound - this does not have to be in the viewport, but in your content browser



## Fire Flicker Function

![](./images/fireflicker.png)





## Fire Flicker Function Call

This is called from the level blueprint

![](./images/FireFunctionCall.png)

<div style="page-break-after: always; break-after: page;"></div>

## Alternate Version - Three Fires One Function

```{Note}
The point light for the fire is passed into the function for each different fire.
```

![](./images/FireFlicker_passinpointlight.png)

Note a local variable has been created for a point light



![](./images/FireFlicker_passinpointlight_input.png)
Note a point light input has been created for the function

![](./images/ThreeFiresOneFunction.png)

