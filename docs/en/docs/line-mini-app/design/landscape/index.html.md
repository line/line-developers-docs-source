# Safe area of LINE MINI App

To make every part of your LINE MINI App visible, even on devices with a notch, we recommend to use CSS to contain LINE MINI App in safe area.
LINE MINI App supports both normal mode and landscape mode. Normal mode and landscape mode require different safe areas.

Set the padding of the LINE MINI App page as follows:

<!-- table of contents -->

## For normal mode 

- Bottom: 34px

Example padding:
```
{
  padding-bottom: 34px;
}
```

![](https://developers.line.biz/media/line-mini-app/mini_design_safearea_normal.png)

## For landscape mode 

- Left and right: 44px
- Bottom: 21px

Example padding:
```
{
  padding-right: 44px;
  padding-bottom: 21px;
  padding-left: 44px;
}
```

![](https://developers.line.biz/media/line-mini-app/mini_design_safearea_landscape.png)
