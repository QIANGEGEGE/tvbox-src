# TVBox 閰嶇疆锛堜節鑱旂洅瀛?/ Android 4.4 / 1GB锛?
## 鐢熸晥閰嶇疆

鐩掑瓙涓婄殑瀹為檯閰嶇疆鏂囦欢锛歚/data/local/tvbox_cfg/tvbox.json`锛?32 瀛楄妭锛?鐢辩洅瀛愭湰鏈?busybox httpd 鍦?`8899` 绔彛浠?*鏄庢枃 HTTP** 鎻愪緵锛孴VBox 閰嶇疆鍦板潃濉細

```
http://127.0.0.1:8899/tvbox.json
```

## 鍏抽敭鐐癸細lives / parses 涓嶈兘鏄┖鏁扮粍

TVBox 瑙ｆ瀽閰嶇疆鍚庝細鐩存帴鎵ц `lives.get(0)`銆傝嫢鍐欐垚 `"lives":[]` 浼氭姏
`IndexOutOfBoundsException: Invalid index 0, size is 0`锛屽鑷?*鏁翠釜閰嶇疆瑙ｆ瀽澶辫触**锛?琛ㄧ幇涓哄紑鏈哄脊銆岃В鏋愰厤缃け璐ャ€嶃€佺珯鐐规暟涓?0銆佹悳绱㈡棤缁撴灉銆?
鎵€浠ユ湰閰嶇疆閲?`lives` 鍜?`parses` 鍚勬斁浜嗕竴涓崰浣嶉」锛堜笉褰卞搷鐐规挱浣跨敤锛夈€?
## 涓轰粈涔堜笉鐢?https

鐩掑瓙鏄?Android 4.4锛孴VBox 鍐呯疆鐨?OkHttp 3.15 + 绯荤粺 TLS 鎻′笉涓婄幇浠?CDN
锛圕loudflare 绛夛級鐨勮瘉涔︿笌 cipher锛岃〃鐜颁负閰嶇疆鎷夊彇澶辫触锛涜€?App 鑷甫鐨?X5 鍐呮牳
锛堢幇浠?BoringSSL锛夊嵈鑳芥甯告墦寮€鍚屼竴鍦板潃鈥斺€旀墍浠ヤ笉鏄綉缁滈棶棰橈紝鏄?TLS 鏍堝お鑰併€?鏀圭敤鏄庢枃 HTTP锛坙oopback + busybox httpd锛夊彲瀹屽叏缁曞紑銆?
busybox httpd 瀵归潤鎬佹枃浠惰繑鍥?`Content-Length`锛岃繖涓€鐐瑰緢鍏抽敭锛?TVBox 鑷甫鐨?9978 鏈嶅姟 `/file/` 璧扮殑鏄?chunked锛岃€?OkHttp 璇?chunked 浼氳绌猴紝
鎵€浠ヤ笉鑳界敤 9978 鑷墭绠°€?
## 寮€鏈鸿嚜鍚?
鐩掑瓙 ROM锛圚iSilicon bigfish / Android 4.4锛夌殑 init 鑴氭湰鍦ㄦ牴鐩綍 `/init.bigfish.rc`锛?鍏?`bigfish-setup` 鏈嶅姟寮€鏈轰互 root 鎵ц `/system/etc/init.bigfish.sh`锛坥neshot锛夈€?璇ヨ剼鏈湯灏捐拷鍔犱簡锛?
```sh
/system/bin/busybox mkdir -p /data/local/tvbox_cfg
if [ -f /data/local/tvbox_cfg/tvbox.json ]; then
  /system/bin/busybox pkill -f "httpd -p 8899" 2>/dev/null
  /system/bin/busybox httpd -p 8899 -h /data/local/tvbox_cfg
fi
```

## 宸查獙璇?
- 閲嶅惎鐩掑瓙鍚?httpd 鑷姩璧锋潵锛岀鍙?8899 LISTEN
- 鎵撳紑 TVBox 鏃犱换浣曞脊绐楋紝婧愮珯涓庡垎绫绘甯稿姞杞?- 鑱氬悎鎼滅储鍙敤锛堛€婄媯椋欍€嬨€婂簡浣欏勾銆嬪潎鏈夌粨鏋滐紝娴锋姤姝ｅ父锛?- 璇︽儏椤?鈫?閫夐泦 鈫?鍏ㄥ睆鎾斁姝ｅ父锛?080p 纭В锛屼腑鏂囧瓧骞曟甯?