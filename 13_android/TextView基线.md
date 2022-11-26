## TextView基线

### 参数解析

1. baseline：文字基线
2. ascent：基线以上文字高度，负值，相对baseline
3. descent：基线以下文字高度，正值，相对baseline
4. leading：文字上方的特殊符号，例如汉语中拼音声调

ps：baseline以上的数据为负值，baseline以下的位置为正值，例：ascent通常为负值，descent通常为正值

### 文字高度

文字高度 = ascent + descent + leading

通常在绘制文字及英文时，leading为0，所以可以不考虑leading的值

文字高度 = ascent + descent

### 中线位置

中线位置 = (bottom - top) / 2 = (ascent + descent) / 2

note：ascent为负值，需要转化成绝对值进行运算

### 中线到基线距离

中线到基线的距离 = 中线位置 - descent = (ascent + descent) / 2 - descent = (ascent - descent) / 2

### 基线位置

基线位置 = 中线位置 + 中线到基线的距离

~~~java
/**
 * 获取基线位置
 */
public float getBaseline(Paint p) {
    Paint.Metrics fm = p.getFontMetrics();
    // 中线位置 + 中线到基线位置
    return (fm.bottom - fm.top) / 2 + (Math.abs(fm.ascent) + fm.descent) / 2 - fm.descent;
}
~~~

**note：ascent、descent的正负值只是相对于baseline而言，实际上文本的坐标原点在左上角（0, 0），基线位置在（0， baseline）**

### 参考链接

[https://www.jianshu.com/p/057ce6b81c52](https://www.jianshu.com/p/057ce6b81c52)
