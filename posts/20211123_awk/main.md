---  
Keywords: awk, gawk  
Copyright: (C) 2021 Toshiya Kiyokawa  
---  
# AWKについてのTips  

## これは何？  
AWKを使っていて気になったことを記載していく。  
- はまったこと  
- 参考になったこと  
- その他  

## Tips
- AWKの真偽判定と左辺値について  
　AWKの真偽判定は  
    - 空文字または数字の0ならば偽  
    - 上記以外はすべて真  
  AWKは左辺値が偽の場合、なにも表示しない  
    `echo "a b c" | awk '1'`  
    a b c  
    `echo "a b c" | awk 'a=0'` ←左辺値が0(偽)のため、何も表示されない  
    `echo "a b c" | awk 'a=1'`  
    a b c  

- lint機能  
    `gawk --lint`
- デバッガ  
    `gawk -D -f xxxxx.awk`  
    ※ デバッガは、-f指定時のみ有効  
(参考URL)[gawk Debugger](http://nethackwiki.com/wiki/User:Paxed/HowTo_setup_dgamelaunch)  
- 改行コードには気をつけろ!(特にWinのデータを扱う際)  
    バグが見つけられなかった時、デバッガで変数を見たら末尾に"/r"を見つけた。  
    元データをExcelで作成後CSVで保存していたことを思いだし、これを削除したら無事動いた。
    
