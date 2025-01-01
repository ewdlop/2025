Creating fireworks effects across various graphics programming languages and environments (HLSL, GLSL, SPIR-V, Metal, Canvas/JavaScript, and SVG) involves implementing particle systems to simulate the behavior of firework explosions. Here's an overview of how this can be approached in each of the specified platforms:

---

### **1. HLSL (High-Level Shading Language)**

HLSL is used for DirectX shaders. Here's a simple example of a firework effect in HLSL:
```hlsl
float4 main(float4 position : SV_POSITION, float4 color : COLOR) : SV_TARGET {
    float time = position.x + position.y; // Pseudo time variable
    float dist = length(position.xy);
    float intensity = exp(-dist * 2.0) * sin(time * 10.0);
    return float4(intensity, intensity * color.r, intensity * color.g, 1.0);
}
```

---

### **2. GLSL (OpenGL Shading Language)**

GLSL is used for OpenGL. Here’s an example:
```glsl
#version 330 core
out vec4 FragColor;

in vec2 FragPos;
uniform float time;

void main() {
    float dist = length(FragPos);
    float intensity = exp(-dist * 10.0) * sin(time * 10.0);
    FragColor = vec4(intensity, intensity * 0.5, intensity * 0.2, 1.0);
}
```

---

### **3. SPIR-V (Shader Portable Intermediate Representation)**

SPIR-V is a binary intermediate representation for Vulkan shaders. Writing SPIR-V directly is uncommon; instead, shaders are written in GLSL or HLSL and compiled to SPIR-V. Here's a GLSL example compiled to SPIR-V:
```glsl
#version 450
layout(location = 0) in vec2 FragPos;
layout(location = 0) out vec4 FragColor;
layout(push_constant) uniform PushConstants {
    float time;
} pc;

void main() {
    float dist = length(FragPos);
    float intensity = exp(-dist * 10.0) * sin(pc.time * 10.0);
    FragColor = vec4(intensity, intensity * 0.5, intensity * 0.2, 1.0);
}
```

---

### **4. Metal**

Metal shaders use the Metal Shading Language (MSL). Here's a simple example:
```metal
#include <metal_stdlib>
using namespace metal;

fragment float4 fireworkShader(float2 position [[position]], constant float &time [[buffer(0)]]) {
    float dist = length(position);
    float intensity = exp(-dist * 10.0) * sin(time * 10.0);
    return float4(intensity, intensity * 0.5, intensity * 0.2, 1.0);
}
```

---

### **5. Canvas (JavaScript)**

For fireworks in Canvas, you would create a particle system:
```javascript
const canvas = document.getElementById("fireworksCanvas");
const ctx = canvas.getContext("2d");

function drawFirework(x, y, radius, time) {
    for (let i = 0; i < 100; i++) {
        const angle = Math.random() * Math.PI * 2;
        const speed = Math.random() * radius;
        const px = x + Math.cos(angle) * speed;
        const py = y + Math.sin(angle) * speed;
        ctx.fillStyle = `rgba(255, ${Math.random() * 255}, 0, ${1 - time})`;
        ctx.beginPath();
        ctx.arc(px, py, 2, 0, Math.PI * 2);
        ctx.fill();
    }
}
```

---

### **6. SVG**

For SVG, you can create fireworks by animating circles and lines:
```html
<svg width="500" height="500">
    <circle cx="250" cy="250" r="0" fill="red">
        <animate attributeName="r" from="0" to="100" dur="1s" fill="freeze" />
        <animate attributeName="opacity" from="1" to="0" dur="1s" fill="freeze" />
    </circle>
</svg>
```

---

Each of these environments has its strengths, and you can adapt the approach depending on your specific use case. Let me know which one you'd like to dive deeper into, and I can provide further elaboration!
