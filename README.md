### 各ファイルについて
- loudness_velocity  
ヴェロシティ毎のラウドネスを測定する Reaper の JS プラグインです。  
[ReaJS](https://www.reaper.fm/reaplugs/) は VST プラグインとして利用できるので、他の DAW でも動作すると思います。
- decoder.xlsx  
上記 JS プラグインの測定結果は特殊なフォーマットで保存されるため、そのままでは利用できません。  
このツールを使って測定結果を復元します。同時にグラフも表示されます。  
MS EXCEL と Googleスプレッドシートで動作を確認しています。
- template.x1.RPP
- template.x100.RPP  
測定用のテンプレートです。
測定対象音源にラウンドロビンなどの機能が無いことが明らかな場合は、各ヴェロシティ毎に１回測定すれば十分なので template.x1.RPP を使用します。そうでない場合は template.x100.RPP を使用します。こちらは100回の平均値を測定結果として採用します。  
第一トラックに測定用の以下の MIDI データが配置されています。第二トラックに測定対象の音源を、第三トラックに loudness_velocity をセットします。時短のためにレンダリングのドライラン実行を使って測定します。
- x1.mid
- x100.mid  
Reaper 以外の DAW を使用する場合には、こちらのMIDIファイルを直接利用してください。
上記テンプレートの第一トラックに配置されているものと同じ内容です。

### loudness_velocity のインストール
ダウンロードした loudness_velocity を次のように配置してください。
```
C:\Users\<someone>\AppData\Roaming\REAPER\Effects\000\loudness_velocity  
```

### MIDI データについて

### 測定手順
