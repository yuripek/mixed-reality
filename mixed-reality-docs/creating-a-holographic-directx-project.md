---
title: Creating a holographic DirectX project
description: Explains how to create a new holographic app based on the Windows Mixed Reality app template.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, holographic app, new app, UWP app, template app, holograms, new project, walkthrough, download, sample code
---



# Creating a holographic DirectX project

A holographic app you create for a HoloLens will be a <a href="https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide" target="_blank">Universal Windows Platform (UWP) app</a>.  If targeting desktop Windows Mixed Reality headsets, you can create a UWP app or a Win32 app.

The DirectX 11 holographic UWP app template is much like the DirectX 11 UWP app template; it includes a program loop (or "game loop"), a **DeviceResources** class to manage the Direct3D device and context, and a simplified content renderer class. It also has an <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview" target="_blank">IFrameworkView</a>, just like any other UWP app.

The mixed reality app, however, has some additional capabilities that aren't present in a typical Direct3D 11 UWP app. The Windows Holographic app template is able to:
* Handle Direct3D device resources associated with holographic cameras.
* Retrieve camera back buffers from the system.
* Handle [gaze](gaze-and-commit.md) input, and recognize a simple [gesture](gestures.md).
* Go into full-screen stereo rendering mode.

## How do I get started?

First [install the tools](install-the-tools.md), following the instructions on downloading Visual Studio 2019 and the Microsoft HoloLens emulator. The holographic app templates are included in the same installer as the Microsoft HoloLens emulator. Also ensure that the option to install the templates is selected before installing.

Now you're ready to create your DirectX 11 Windows Mixed Reality app! Note, to remove the sample content, comment out the **DRAW_SAMPLE_CONTENT** preprocessor directive in *pch.h*.

## Creating a UWP project

Once the [tools are installed](install-the-tools.md) you can then create a holographic DirectX UWP project.

To create a new project:
1. Start **Visual Studio**.
2. From the **File** menu, point to **New** and select **Project** from the context menu. The **New Project** dialog opens.
3. Expand **Installed** on the left and expand the **Visual C++** language node.
4. Navigate to the **Windows Universal > Holographic** node and select **Holographic DirectX 11 App (Universal Windows) (C++/WinRT)**.
   ![Screenshot of the Holographic DirectX 11 C++/WinRT UWP app project template in Visual Studio](images/holographic-directx-app-cpp-new-project.png)<br>
   *Holographic DirectX 11 C++/WinRT UWP app project template in Visual Studio*
   >[!IMPORTANT]
   >Be sure that the project template's name includes "(C++/WinRT)".  If not, you have an older version of the holographic project templates installed.  To get the latest project templates, [install the latest HoloLens Emulator](using-the-hololens-emulator.md).
5. Fill in the **Name** and **Location** text boxes, and click or tap **OK**. The holographic app project is created.
6. For development targeting only HoloLens 2, ensure that the **Target version** and **Minimum version** are set to **Windows 10, version 1903**.  If you are also targeting HoloLens (1st gen) or desktop Windows Mixed Reality headsets, you can set **Minimum version** to **Windows 10, version 1809** instead, although this will require some <a href="https://docs.microsoft.com/windows/uwp/debug-test-perf/version-adaptive-code" target="_blank">version adaptive checks</a> in your code when using new features of HoloLens 2.
   ![Screenshot of setting Windows 10, version 1903 as the target and minimum versions](images/new-uwp-project.png)<br>
   *Setting **Windows 10, version 1903** as the target and minimum versions*
   >[!IMPORTANT]
   >If you do not see **Windows 10, version 1903** as an option, you do not have the latest Windows 10 SDK installed.  To get this option to appear, <a href="https://developer.microsoft.com/en-US/windows/downloads/windows-10-sdk" target="_blank">install version 10.0.18362.0 or later of the Windows 10 SDK</a>.

The template generates a project using <a href="https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/" target="_blank">C++/WinRT</a>, a C++17 language projection of the Windows Runtime APIs that supports any standards-compliant C++17 compiler.  The project shows how to create a world-locked cube that's placed two meters from the user. The user can [air-tap](gestures.md#air-tap) or press a button on the controller to place the cube in a different position that's specified by the user's [gaze](gaze-and-commit.md). You can modify this project to create any mixed reality app.

Alternatively, you can create a new project using the **Visual C#** holographic project template, which is based on SharpDX.  If your holographic C# project did not start from the Windows Holographic app template, you will need to copy the ms.fxcompile.targets file from a Windows Mixed Reality C# template project and import it in your .csproj file in order to compile HLSL files that you add to your project.

Review [Using Visual Studio to deploy and debug](using-visual-studio.md) for information on how to build and deploy the sample to your HoloLens, PC with immersive device attached, or an emulator.

The rest of the instructions below will assume that you are using C++ to build your app.

### UWP app entry point

Your holographic UWP app starts in the **wWinMain** function in AppView.cpp. The **wWinMain** function creates the app's <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview" target="_blank">IFrameworkView</a> and starts the <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication" target="_blank">CoreApplication</a> with it.

From **AppView.cpp**:

```cpp
// The main function bootstraps into the IFrameworkView.
int __stdcall wWinMain(HINSTANCE, HINSTANCE, PWSTR, int)
{
    winrt::init_apartment();
    CoreApplication::Run(AppViewSource());
    return 0;
}
```

From that point on, the AppView class handles interaction with Windows basic input events, CoreWindow events and messaging, and so on. It will also create the HolographicSpace used by your app.

## Creating a Win32 project

The easiest way to get started building a Win32 holographic project is to adapt the <a href="https://github.com/Microsoft/Windows-classic-samples/tree/master/Samples/BasicHologram" target="_blank">*BasicHologram* Win32 sample</a>.

This Win32 sample uses <a href="https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/" target="_blank">C++/WinRT</a>, a C++17 language projection of the Windows Runtime APIs that supports any standards-compliant C++17 compiler.  The project shows how to create a world-locked cube that's placed two meters from the user. The user can press a button on the controller to place the cube in a different position that's specified by the user's [gaze](gaze-and-commit.md). You can modify this project to create any mixed reality app.

### Win32 app entry point

Your holographic Win32 app starts in the **wWinMain** function in AppMain.cpp. The **wWinMain** function creates the app's HWND and starts its message loop.

From **AppMain.cpp**:

```cpp
int APIENTRY wWinMain(
    _In_     HINSTANCE hInstance,
    _In_opt_ HINSTANCE hPrevInstance,
    _In_     LPWSTR    lpCmdLine,
    _In_     int       nCmdShow)
{
    UNREFERENCED_PARAMETER(hPrevInstance);
    UNREFERENCED_PARAMETER(lpCmdLine);

    winrt::init_apartment();

    App app;

    // Initialize global strings, and perform application initialization.
    app.Initialize(hInstance);

    // Create the HWND and the HolographicSpace.
    app.CreateWindowAndHolographicSpace(hInstance, nCmdShow);

    // Main message loop:
    app.Run(hInstance);

    // Perform application teardown.
    app.Uninitialize();

    return 0;
}
```

From that point on, the AppMain class handles interaction with basic window messages, and so on. It will also create the HolographicSpace used by your app.

## Render holographic content

The project's **Content** folder contains classes for rendering holograms in the [holographic space](getting-a-holographicspace.md). The default hologram in the template is a spinning cube that's placed two meters away from the user. Drawing this cube is implemented in **SpinningCubeRenderer.cpp**, which has these key methods:

|  Method  |  Explanation | 
|----------|----------|
|  `CreateDeviceDependentResources` |  Loads shaders and creates the cube mesh. | 
|  `PositionHologram` |  Places the hologram at the location specified by the provided <a href="https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerpose" target="_blank">SpatialPointerPose</a>. | 
|  `Update` |  Rotates the cube, and sets the model matrix. | 
|  `Render` |  Renders a frame using the vertex and pixel shaders. | 

The **Shaders** subfolder contains four default shader implementations:

|  Shader  |  Explanation | 
|----------|----------|
|  `GeometryShader.hlsl` |  A pass-through that leaves the geometry unmodified. | 
|  `PixelShader.hlsl` |  Passes through the color data. The color data is interpolated and assigned to a pixel at the rasterization step. | 
|  `VertexShader.hlsl` |  Simple shader to do vertex processing on the GPU. | 
|  `VPRTVertexShader.hlsl` |  Simple shader to do vertex processing on the GPU, that is optimized for Windows Mixed Reality stereo rendering. | 

`VertexShaderShared.hlsl` contains common code shared between `VertexShader.hlsl` and `VPRTVertexShader.hlsl`.

The shaders are compiled when the project is built, and they're loaded in the **SpinningCubeRenderer::CreateDeviceDependentResources** method.

## Interact with your holograms

User input is processed in the **SpatialInputHandler** class, which gets a <a href="https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionmanager" target="_blank">SpatialInteractionManager</a> instance and subscribes to the <a href="https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed" target="_blank">SourcePressed</a> event. This enables detecting the air-tap gesture and other spatial input events.

## Update holographic content

Your mixed reality app updates in a game loop, which by default is implemented in the **Update** method in `AppMain.cpp`. The **Update** method updates scene objects, like the spinning cube, and returns a <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> object that is used to get up-to-date view and projection matrices and to present the swap chain.

The **Render** method in `AppMain.cpp` takes the <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> and renders the current frame to each holographic camera, according to the current app and spatial positioning state.

## See also
* [Getting a HolographicSpace](getting-a-holographicspace.md)
* <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspaceh" target="_blank">HolographicSpace</a>
* [Rendering in DirectX](rendering-in-directx.md)
* [Using Visual Studio to deploy and debug](using-visual-studio.md)
* [Using the HoloLens emulator](using-the-hololens-emulator.md)
* [Using XAML with holographic DirectX apps](using-xaml-with-holographic-directx-apps.md)
