## 使用控制器 

本教程将介绍：

1. 引入和跟踪控制器对象。

2. 使用控制器事件API，与 Unity UI 系统交互。

控制器具有以下特性:

- 无需加载标定文件。 控制器通过蓝牙配对后， 系统根据 控制器的SN编号，自动索引控制器标定文件。

- 支持 Trigger , TouchPad, App, Home 四个按键， 和触摸盘位置信息。




# Controller UI 场景

1. 打开 Assets/Demo/Scenes/Controller UI.unity 场景。这个简单的场景有以下对象:

- ARCamera

- Canvas - 一个标准的 UI canvas。 

## RxController 组件

![Logo](https://raw.githubusercontent.com/yinyuanqings/AIOSDK/gh-pages/img/Controller-Unity.png ':size=450X400')

![Logo](https://raw.githubusercontent.com/yinyuanqings/AIOSDK/gh-pages/img/RxControllerInspector.png ':size=450X400')

         
```bash
//RxController 是控制器的事件接口。 通过如下代码可以访问控制的事件API: 
//更详细的接口说明， 请参见API文档部分. 

    RXController controller = GetComponent<RXController>();
    controller.OnTap.AddListener((ControllerButtonCode btn) => {
        Debug.LogFormat("On controller tap : {0}", btn);
    });
            
```

> RxController 的 Raycast 对象定义了和 UI 的交互射线。



![Logo](https://raw.githubusercontent.com/yinyuanqings/AIOSDK/gh-pages/img/RxControllerInspector.png ':size=450X400')




## RxEventSystem 组件.

![Logo](https://raw.githubusercontent.com/yinyuanqings/AIOSDK/gh-pages/img/RxEventSystem-Inspector.png ':size=450X400')

> RxEventSystem 是 Controller 系统事件驱动的核心组件，场景中必须存在此组件，事件机制才会工作。

> 开发者可以配置 RxInputModule上的 Pointer Button，定义与Unity UI系统交互的按键。

!> RxEventSystem 事件继承于 UnityEngine.EventSystem 对象，与Unity自带的EventSystem对象冲突， 所以请删除unity自动创建的EventSystem对象(SDK程序会在运行时自动删除)


## RxRaycast 组件

![Logo](https://raw.githubusercontent.com/yinyuanqings/AIOSDK/gh-pages/img/RxRaycaster-Inspector.png ':size=450X400')

> RxRaycast组件定义射线的起点和方向。 它可以和Unity内置的事件系统一起工作。
> 设置 EventMask 和 Raycast Distance 以定义交互对象的层级和射线的长度。

```bash
//以下代码示例使用Unity的事件系统和RxController协同工作。 

public class EventListenerDemo : MonoBehaviour, IPointerDownHandler, IPointerUpHandler, IPointerClickHandler, IPointerEnterHandler, IPointerExitHandler
{
    public void OnPointerClick(PointerEventData eventData)
    {
        Debug.LogFormat(this, "Click : {0}", name);
    }

    public void OnPointerDown(PointerEventData eventData)
    {
        Debug.LogFormat(this, "Down : {0}", name);
    }

    public void OnPointerEnter(PointerEventData eventData)
    {
        Debug.LogFormat(this, "Enter : {0}", name);
    }

    public void OnPointerExit(PointerEventData eventData)
    {
        Debug.LogFormat(this, "Exit : {0}", name);
    }

    public void OnPointerUp(PointerEventData eventData)
    {
        Debug.LogFormat(this, "Up : {0}", name);
    }
}
            
```

- 我们已经知道了 Controller 的基本使用方式。 接下来请编译并安装 Controller UI 场景，体验使用 Controller 在AR场景中的交互方式吧 ！