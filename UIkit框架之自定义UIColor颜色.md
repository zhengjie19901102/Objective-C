## UIkit框架之自定义UIColor颜色

```objc
/*
 * 参数解释:
 * @param red -> 红色通道
 * @param green -> 绿色通道
 * @param blue -> 蓝色通道
 * @param alpha -> 透明度通道
 * 在方法中实际接收的四项参数都为float类型，所以对应32位颜色通道需要除以255
 * 注意: 如果两边进行计算的数字都为整数那么按照规则结果也为整数。所以此处要想获取小数需要至少一个浮点数参与运算。
 */

UIColor color = [UIColor colorWithRed:255.0/255 green:0/255.0 blue:0/255.0 alpha:1];
```