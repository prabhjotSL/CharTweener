# CharTweener
Got [DOTween](http://dotween.demigiant.com/index.php)? Got [TextMeshPro](https://assetstore.unity.com/packages/essentials/beta-projects/textmesh-pro-84126)?

Using CharTweener, you can do stuff like this...
![Example](https://github.com/mdechatech/CharTweener/blob/master/Content/example_simple.gif)

Using code like this! (Full script [here](https://github.com/mdechatech/CharTweener/blob/master/Assets/CharTween/Examples/CharTweenExampleSimple.cs))
```c#
private void Start()
{
    // Set text
    var text = GetComponent<TMP_Text>();
    text.text = "DETERMINATION";

    var tweener = text.GetCharTweener();    
    for (var i = 0; i < tweener.CharacterCount; ++i)
    {
        // Move characters in a circle
        var circleTween = tweener.DOCircle(i, 0.05f, 0.5f)
            .SetEase(Ease.Linear)
            .SetLoops(-1, LoopType.Restart);

        // Oscillate character color between yellow and white
        var colorTween = tweener.DOColor(i, Color.yellow, 0.5f)
            .SetLoops(-1, LoopType.Yoyo);

        // Offset animations based on character index in string
        var timeOffset = Mathf.Lerp(0, 1, i / (float)(tweener.CharacterCount - 1));
        circleTween.fullPosition = timeOffset;
        colorTween.fullPosition = timeOffset;
    }
}
```
