# 记事本添加时间戳
1.首先在java文件夹下的com.example.android.notepad里找到一个叫NotesList的文件

![](https://github.com/mimitang/jishiben/blob/master/screenshot/1.png)

在PROJECTION中添加时间

![](https://github.com/mimitang/jishiben/blob/master/screenshot/2.png)

2.然后添加要装配的数据

![](https://github.com/mimitang/jishiben/blob/master/screenshot/3.png)

3.在noteslist_item.xml中再加入

```
<TextView
            android:id="@+id/time"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textAppearance="?android:attr/textAppearanceSmall"
            android:paddingLeft="5dip" />
            
```



在这个地方纠结了挺久时间的，原来一个TextView的时候，文件没出错。再加一个TextView的时候报错了，找了挺多资料的，最终找到的方法是在2个TextView前加入RelativeLayout，把他们2个框起来。加完后发现2个TextView，就能不报错了。![](https://github.com/mimitang/jishiben/blob/master/screenshot/4.png)

4.然后再讲文件中的过时代码进行更新下![](https://github.com/mimitang/jishiben/blob/master/screenshot/5.png)

5.在NotePadProvider.java中再修改这部分代码

```
 		// Gets the current system time in milliseconds
        Long now = Long.valueOf(System.currentTimeMillis());
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String time = sdf.format(new Date(Long.parseLong(String.valueOf(now))));
```

![](https://github.com/mimitang/jishiben/blob/master/screenshot/6.png)

6.修改在NoteEditor.java中

```
// Sets up a map to contain values to be updated in the provider.
        ContentValues values = new ContentValues();
        Long now = Long.valueOf(System.currentTimeMillis());
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String time = sdf.format(new Date(Long.parseLong(String.valueOf(now))));
        values.put(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE, time);
```

![](https://github.com/mimitang/jishiben/blob/master/screenshot/7.png)

7.最后在NoteEditor和NotePadProvider中import所需要的包：

```
import java.text.SimpleDateFormat;
import java.util.Date;
```

8.然后就成功了，运行一下![](https://github.com/mimitang/jishiben/blob/master/screenshot/8.png)
