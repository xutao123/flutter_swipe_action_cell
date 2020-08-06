Language: 
[English](https://github.com/luckysmg/flutter_swipe_action_cell/blob/master/README.md)
|[中文简体](https://github.com/luckysmg/flutter_swipe_action_cell/blob/master/README-CN.md)

# flutter_swipe_action_cell

A package that can give you a cell that can be swiped ,effect is like iOS native

## Why do I want to create this lib?
I like iOS native 's swipe action ,but flutter doesn't give an official widget .
So I try to create one.

## Get started

### pub home page click here: [pub](https://pub.dev/packages/flutter_swipe_action_cell)
### install:
```yaml
flutter_swipe_action_cell: ^1.0.4+1
```  

## Example

Tip:This widget should be put in the itemBuilder of your ListView

 - ##  Example 1:Simple delete the item in ListView
 
 ### (Tip:There is a gif here,if it is unable to load,please go to [GitHub](https://github.com/luckysmg/flutter_swipe_action_cell/blob/master/README.md))
 

 ![](https://github.com/luckysmg/flutter_swipe_action_cell/blob/master/images/1.gif?raw=true)
 
```dart
 SwipeActionCell(
      key: ObjectKey(list[index]),///this key is necessary
      actions: <SwipeAction>[
        SwipeAction(
            title: "delete",
            onTap: (CompletionHandler handler) async {
              list.removeAt(index);
              setState(() {});
            },
            color: Colors.red),
      ],
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Text("this is index of ${list[index]}",
            style: TextStyle(fontSize: 40)),
      ),
    );
```

 - ##  Example 2:Perform first action when full swipe
 
 ![](https://github.com/luckysmg/flutter_swipe_action_cell/blob/master/images/2.gif?raw=true)

 ```dart
 SwipeActionCell(
       ///this key is necessary
       key: ObjectKey(list[index]),
 
       ///this is the same as iOS native
       performsFirstActionWithFullSwipe: true,
       actions: <SwipeAction>[
         SwipeAction(
             title: "delete",
             onTap: (CompletionHandler handler) async {
               list.removeAt(index);
               setState(() {});
             },
             color: Colors.red),
       ],
       child: Padding(
         padding: const EdgeInsets.all(8.0),
         child: Text("this is index of ${list[index]}",
             style: TextStyle(fontSize: 40)),
       ),
     );
 ```

 - ##  Example 3:Delete with animation 
 
  ![](https://github.com/luckysmg/flutter_swipe_action_cell/blob/master/images/3.gif?raw=true)

 ```dart
SwipeActionCell(
      ///this key is necessary
      key: ObjectKey(list[index]),
      ///this name is the same as iOS native
      performsFirstActionWithFullSwipe: true,
      actions: <SwipeAction>[
        SwipeAction(
            title: "delete",
            onTap: (CompletionHandler handler) async {
              
              /// await handler(true) : will delete this row
              ///And after delete animation,setState will called to 
              /// sync your data source with your UI

              await handler(true);
              list.removeAt(index);
              setState(() {});
            },
            color: Colors.red),
      ],
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Text("this is index of ${list[index]}",
            style: TextStyle(fontSize: 40)),
      ),
    );
 ```

  - ## Example 4:More than one action: 
 
  ![](https://github.com/luckysmg/flutter_swipe_action_cell/blob/master/images/4.gif?raw=true)


 ```dart
SwipeActionCell(
      ///this key is necessary
      key: ObjectKey(list[index]),

      ///this name is the same as iOS native
      performsFirstActionWithFullSwipe: true,
      actions: <SwipeAction>[
        SwipeAction(
            title: "delete",
            onTap: (CompletionHandler handler) async {
              await handler(true);
              list.removeAt(index);
              setState(() {});
            },
            color: Colors.red),

        SwipeAction(
            widthSpace: 120,
            title: "popAlert",
            onTap: (CompletionHandler handler) async {
              ///false means that you just do nothing,it will close
              /// action buttons by default
              handler(false);
              showCupertinoDialog(
                  context: context,
                  builder: (c) {
                    return CupertinoAlertDialog(
                      title: Text('ok'),
                      actions: <Widget>[
                        CupertinoDialogAction(
                          child: Text('confirm'),
                          isDestructiveAction: true,
                          onPressed: () {
                            Navigator.pop(context);
                          },
                        ),
                      ],
                    );
                  });
            },
            color: Colors.orange),
      ],
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Text(
            "this is index of ${list[index]}",
            style: TextStyle(fontSize: 40)),
      ),
    );
 ```

  - ## Example 5:Delete like wechat message page(need to confirm it:
    ![](https://github.com/luckysmg/flutter_swipe_action_cell/blob/master/images/6.gif?raw=true)
    
```dart
return SwipeActionCell(
      ///this key is necessary
      key: ValueKey(list[index]),

      ///this is the same as iOS native
      performsFirstActionWithFullSwipe: true,
      actions: <SwipeAction>[
        SwipeAction(
          nestedAction: SwipeNestedAction(title: "确认删除"),
          title: "删除",
          onTap: (CompletionHandler handler) async {
            await handler(true);
            list.removeAt(index);
            setState(() {});
          },
          color: Colors.red,
        ),
        SwipeAction(
            title: "置顶",
            onTap: (CompletionHandler handler) async {
              ///false means that you just do nothing,it will close
              /// action buttons by default
              handler(false);
            },
            color: Colors.grey),
      ],
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Text("this is index of ${list[index]}",
            style: TextStyle(fontSize: 40)),
      ),
    );
```


# About CompletionHandler in onTap function of SwipeAction
it means how you want control this cell after you tap it.
If you don't want any animation,just don't call it and update your data and UI with setState()

If you want some animation:
- handler(true) : Means this row will be deleted(You should call setState after it)

- await handler(true) : Means that you will await the animation to complete(you should call setState after it so that you will get an animation)

- handler(false) : means it will not delete this row.By default,it just close this cell's action buttons.

- await handler(false) : means it will wait the close animation to complete.

# About all parameter:
I wrote them in my code with dart doc comments.You can read them in
source code.

 


