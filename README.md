# 🌍 AGSL — Android Graphics Shading Language Sandbox

<div align="center">

[![Android](https://img.shields.io/badge/Platform-Android_13+-3DDC84?style=for-the-badge&logo=android&logoColor=white)](https://developer.android.com)
[![Kotlin](https://img.shields.io/badge/Kotlin-2.0+-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)](https://kotlinlang.org)
[![AGSL](https://img.shields.io/badge/API-RuntimeShader-FF6F00?style=for-the-badge)](https://developer.android.com/develop/ui/views/graphics/agsl)
[![Compose](https://img.shields.io/badge/Jetpack_Compose-Material_3-4285F4?style=for-the-badge&logo=jetpackcompose&logoColor=white)](https://developer.android.com/jetpack/compose)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)

An experimental Android project exploring **custom GPU shader effects** using **AGSL (Android Graphics Shading Language)** and Jetpack Compose on Android 13+ (API 33+).

</div>

---

## 🎥 Preview

https://github.com/user-attachments/assets/cd213170-7e69-4b28-989c-f55056ef9f8d

---

## ✨ Features

- 🌐 **3D Rotating Globe Effect**: Ray-marched procedural 3D sphere rendered purely in fragment shader code.
- ⚡ **Hardware Accelerated**: Powered by Android's `RuntimeShader` with direct GPU execution via Skia / Vulkan.
- 🎨 **Jetpack Compose Integration**: Seamlessly applied via `.graphicsLayer { renderEffect = ... }` and `Modifier.drawWithCache`.
- 🎛️ **Dynamic Uniforms**: Real-time manipulation of time, resolution, light direction, and surface textures.

---

## 💡 How it Works

AGSL uses GLSL-compatible syntax executing directly on the Android RenderThread:

```kotlin
@Language("AGSL")
val GLOBE_SHADER = """
    uniform float2 iResolution;
    uniform float iTime;
    
    half4 main(in float2 fragCoord) {
        float2 uv = (fragCoord - 0.5 * iResolution) / min(iResolution.x, iResolution.y);
        // Procedural ray-marching & sphere mapping
        float r = length(uv);
        if (r > 0.5) return half4(0.0, 0.0, 0.0, 0.0);
        
        // 3D normal & lighting calculations
        float z = sqrt(0.25 - r * r);
        float3 normal = normalize(float3(uv.x, uv.y, z));
        return half4(normal * 0.5 + 0.5, 1.0);
    }
""".trimIndent()
```

---

## 🚀 Requirements

- Android 13 (API Level 33) or higher
- Android Studio Ladybug or newer
- Kotlin 2.0+

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
