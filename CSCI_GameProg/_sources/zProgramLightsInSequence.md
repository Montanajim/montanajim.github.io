# Program Lights In A Sequence - Using Functions



* **Goal:**
   Create three light sources that illuminate in sequence—1, 2, 3—and then repeat continuously.

------

  **Process:**

  1. Start a new Actor class.
  2. Add three light sources to the viewport.
  3. Store the lights in an array. This allows for easy access to the correct light based on the counter. The counter's **remainder** (counter value modulo 3) will indicate which light to activate.
  4. Create and initialize a counter. Use the **modulus operator** (`%`) to determine which light to turn on.
  5. Turn off all the lights.
  6. Calculate the remainder: `counter % 3`.
  7. Use the remainder value to activate the corresponding light from the array.
  8. Increment the counter.
  9. Repeat the process, starting again with turning off all the lights.



## Viewport



![image-20250908202111297](./assets/ProgramLightsInSequence_ViewPort.png)



Add three light sources to the viewport. You can also configure each lamp's characteristics here, such as intensity, color, or attenuation radius.



## Actor Class - Main Blueprint



###### ![image-20250908201356406](./assets/ProgramLightsInSequence.png)

<!--
```mermaid
flowchart LR

EvtBeginPlay["Event Begin Play"]
SetArray["Set Array"]
StLght0["Set All Lights To 0 Intenstity"]
PL1[Point Light 1]
PL2[Point Light 2]
PL3[Point Light 3]
MKA[Make Array]
GR[Get Remainder]
SLV[Set Light Value]
IC[Increment Counter]
Delay[Delay]


PL1 --- MKA
PL2 --- MKA
PL3 --- MKA


EvtBeginPlay --> SetArray

MKA --- SetArray
SetArray --> StLght0
StLght0 --> GR
GR --> SLV
SLV --> IC
IC --> Delay
Delay --> StLght0
```

-->


---

## Function - Set Light Intensity To Zero

![image-20250908202423015](./assets/ProgramLightsInSequence_LightsZero.png)

---

## Function - Get Remainder - Choose The Correct Array Element (Light)

| Add input and output details



![image-20250908202722840](./assets/ProgramLightsInSequence_Remainder.png)

![image-20250910095146145](./assets/ProgramLightsInSequence_GetRemainder_reva.png)

![image-20250910122724641](./assets/ProgramLightsInSequence_StartNode_I.png)

![image-20250910122433979](./assets/ProgramLightsInSequence_ReturnNode_I.png)

---

## Set Selected Light Values

![image-20250908203928200](./assets/ProgramLightsInSequence_SetSelectedLightValues.png)



![image-20250908204311940](./assets/ProgramLightsInSequence_SetSelectedLightValues_A.png

![image-20250910122946631](./assets/ProgramLightsInSequence_SetSelectedLightValues_I.png)

---





