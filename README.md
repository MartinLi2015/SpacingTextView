
# SpacingTextView
字距为任何字符串的TextView,设置文本间距
    关于我，欢迎关注~
 [我的博客](http://blog.csdn.net/u011974987) 
* 项目描述：
    字距为任何字符串的TextView,设置文本间距,在网上找了许多方法都不可行，就弄个笔记记录下来，方便以后使用。放在[GitHub](https://github.com/git-xuhao) 上面了。

* 本Demo效果截图示例如下：

 ![](https://github.com/git-xuhao/SpacingTextView/blob/master/SpacingTextView/device-2016-03-07-171918.png)  
 
核心代码：
---------

```Java
package com.woyou.spacingtextview;

import android.content.Context;
import android.text.Spannable;
import android.text.SpannableString;
import android.text.style.ScaleXSpan;
import android.util.AttributeSet;
import android.widget.TextView;

/**
 * Created by Xiho on 2016/3/7.
 */
public class SpacingTextView extends TextView{
    private float letterSpacing = LetterSpacing.BIGGEST;
    private CharSequence originalText = "";


    public SpacingTextView(Context context) {
        super(context);
    }

    public SpacingTextView(Context context, AttributeSet attrs){
        super(context, attrs);
        originalText = super.getText();
        applyLetterSpacing();
        this.invalidate();
    }

    public SpacingTextView(Context context, AttributeSet attrs, int defStyle){
        super(context, attrs, defStyle);
    }

    public float getLetterSpacing() {
        return letterSpacing;
    }

    public void setLetterSpacing(float letterSpacing) {
        this.letterSpacing = letterSpacing;
        applyLetterSpacing();
    }

    @Override
    public void setText(CharSequence text, BufferType type) {
        originalText = text;
        applyLetterSpacing();
    }

    @Override
    public CharSequence getText() {
        return originalText;
    }

    /**
     * 字距为任何字符串（技术上，一个简单的方法为CharSequence不使用）的TextView
     */
    private void applyLetterSpacing() {
        if (this == null || this.originalText == null) return;
        StringBuilder builder = new StringBuilder();
        for(int i = 0; i < originalText.length(); i++) {
            String c = ""+ originalText.charAt(i);
            builder.append(c.toLowerCase());
            if(i+1 < originalText.length()) {
                builder.append("\u00A0");
            }
        }
        SpannableString finalText = new SpannableString(builder.toString());
        if(builder.toString().length() > 1) {
            for(int i = 1; i < builder.toString().length(); i+=2) {
                finalText.setSpan(new ScaleXSpan((letterSpacing+1)/10), i, i+1, Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
            }
        }
        super.setText(finalText, BufferType.SPANNABLE);
    }

    public class LetterSpacing {
        public final static float NORMAL = 0;
        public final static float NORMALBIG = (float)0.025;
        public final static float BIG = (float)0.05;
        public final static float BIGGEST = (float)0.2;
    }
}


```

##Thanks!

*[SpacingTextView](https://github.com/git-xuhao/SpacingTextView)

