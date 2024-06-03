## 获取 FragmentManager
- FragmentActivity 及其子类通过 getSupportFragmentManager()
- Fragment 通过 getChildFragmentManager()
- 子 Fragment 通过 getParentFragmentManager() 

![](../img/Fragment_1.png)

## 使用 FragmentManager


## Fragment 事务
- add() 此方法会收到用于存储此 Fragment 的容器 ID ，以及您要添加的 Fragment 的类名。添加的 Fragment 会转为 RESUMED 状态
- remove() 此方法用于移除 Fragment ，移除通过 findFragmentById() 或 findFragmentByTag() 从 FragmentManager 检索到的 Fragment 实例。已移除的 Fragment 会转为 DESTROYED 状态
- replace() 将容器现有的 Fragment 替换为提供的新 Fragment 实例。调用 replace() 等同于对容器中的 Fragment 调用 remove() 后将新的 Fragment 添加到同一容器中。
- show() 和 hide() 显示和隐藏已添加至容器的 Fragment ，可设置 Fragment 视图的可见性，而不会影响 Fragment 的生命周期。