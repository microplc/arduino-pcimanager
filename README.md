# 介绍 #

使用 PciManager 库你能管理微控制器的引脚中断 Pin Change Interrupt 。
你可以在 PciManager 中注册监听一个引脚的变化，管理器处理中断并召唤监听者。

PciManager 并不读取引脚值，他只是隐藏了烦人的硬件标识，但足够处理多个引脚多个变化。

注意: 在一些硬件上，引脚变化中断并没有被中断向量所声明，而 PciManager 运行需要中断向量，在这样的硬件上它也不会正常工作。


# 示例代码 #

```
#include <PciManager.h>
#include <PciListenerImp.h>

#define INPUT_PIN 3

PciListenerImp listener(INPUT_PIN, onPinChange);


void setup() {
  Serial.begin(9800);
  PciManager.registerListener(INPUT_PIN, &listener);
  Serial.println("Ready.");
}

void onPinChange(byte changeKind) {
  Serial.print("pci : ");
  Serial.println(changeKind);
}

void loop() { }
```
