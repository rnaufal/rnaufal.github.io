---
id: 54
title: 'Swing tips and tricks'
guid: 'http://rnaufal.wordpress.com/2007/11/19/swing-tips-and-tricks/'
lj_itemid:
    - '62'
lj_permalink:
    - 'http://rnaufal.livejournal.com/16021.html'
dsq_thread_id:
    - '102751803'
categories:
    - Uncategorized
tags:
    - java
    - programming
    - swing
---

Some days go I was given the task to customize the Java Swing widgets for a project in our company. The default look and feel of a [JDialog](http://java.sun.com/javase/6/docs/api/javax/swing/JDialog.html), specifically, has the [Java](http://java.sun.com) logo trademark icon on the upper corner left, the close button on the right one and the title panel is painted according to the default [MetalLookAndFeel](http://java.sun.com/j2se/1.5.0/docs/api/javax/swing/plaf/metal/MetalLookAndFeel.html) probably. As an example, we have something like this:

We wanna have an option to change the title’s panel color, to remove the close button and not to have the Java trademark logo showing on the panel. The final JDialog should look like this:

I’ve thought it was a nearly difficult task, because I had to override a default look and feel and some hidden properties, sometimes difficult to find. Shame on me. Searching through some forums, I’ve found some interesting tips and tricks about how to customize a the entire dialogs of a Swing application, even without creating a look and feel or overriding an old one.

For your knowledge, here are some overridden properties to make the JDialog seems like the latter above. These properties let you define new colors for the active caption of your widgets, other font colors, custom family types and much more (for other properties see through the documentation API or the forums below).

```java
UIManager.put("activeCaption", Color.BLUE);
UIManager.put("activeCaptionText", Color.WHITE);
UIManager.put("InternalFrame.titleFont", new Font("Arial-12-i-2", Font.BOLD, 11));
Border cuverdBorder = new LineBorder(new Color(210, 210, 210), 2, true);
dialog.getRootPane().setBorder(cuverdBorder);
dialog.getRootPane().setWindowDecorationStyle(JRootPane.PLAIN_DIALOG);
JDialog.setDefaultLookAndFeelDecorated(true);
JFrame.setDefaultLookAndFeelDecorated(true);
dialog.setUndecorated(true);
```

As a little example, below is the Java code to remove the close button from the panel’s title. This little code snippet below traverses the component hierarchy, passed as a parameter, in a recursive method.

```java
public static void removeCloseButton(Component comp) {
    if (comp instanceof AbstractButton) {
        Action action = ((AbstractButton) comp).getAction();
        String cmd = (action == null) ? "" : action.toString();
        if (cmd.contains("CloseAction")) {
            comp.getParent().remove(comp);
        }
    } else if (comp instanceof Container) {
        Component[] children = ((Container) comp).getComponents();
        for (int i = 0; i < children.length; ++i) {
            removeCloseButton(children[i]);
        }
    }
}
```

Here are some Sun forums I’ve searched so far to find the possible helps for this solution:

- <http://forum.java.sun.com/thread.jspa?threadID=630096>
- [http://forum.java.sun.com/thread.jspa?threadID=690852&amp;messageID=4016833](http://forum.java.sun.com/thread.jspa?threadID=690852&messageID=4016833)
- [http://forum.java.sun.com/thread.jspa?forumID=54&amp;threadID=501146](http://forum.java.sun.com/thread.jspa?forumID=54&threadID=501146)
- [http://forum.java.sun.com/thread.jspa?threadID=356373&amp;messageID=1486015](http://forum.java.sun.com/thread.jspa?threadID=356373&messageID=1486015)
- [http://forum.java.sun.com/thread.jspa?threadID=5171154&amp;messageID=9658560](http://forum.java.sun.com/thread.jspa?threadID=5171154&messageID=9658560)
- [http://forum.java.sun.com/thread.jspa?threadID=765742&amp;messageID=4366238](http://forum.java.sun.com/thread.jspa?threadID=765742&messageID=4366238)

Hope you make use of those tricks in your projects :-).