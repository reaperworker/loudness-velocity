### 各ファイルについて
- loudness_velocity  
ヴェロシティ毎のラウドネスを測定する Reaper の JS プラグインです。  
[ReaJS](https://www.reaper.fm/reaplugs/) は VST プラグインとして利用できるので、他の DAW でも動作すると思います。  
**第一チャンネルLのみを測定する簡易なツールです。音源の出力 L+R がツールのLに入力されるようにしてください。**
- decoder.xlsx  
上記 JS プラグインの測定結果は特殊なフォーマットで保存されるため、そのままでは利用できません。  
このツールを使って測定結果を復元します。同時にグラフも表示されます。  
MS EXCEL と Googleスプレッドシートで動作を確認しています。
- template.x1.RPP
- template.x100.RPP  
Reaper 用のテンプレートです。
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
測定対象の音符データがMIDIチャンネル1に記録され、ツール制御用のデータがMIDIチャンネル10に記録されています。  
制御用データで音が鳴ってしまわないように、チャンネル1のデータのみを測定対象音源の入力とします。全てのMIDIデータと音源が出力するオーディオデータ双方を loudness_velocity の入力とします。
（Reaper 用のテンプレートの各トラックは、既にそのように設定されています。）  
ツール制御用のデータは次のとおりです。
- D#-1(003) 平均値の初期化
- D-1(002)　ツール全体の初期化
- C#-1(001) 最大値の初期化

### 測定手順
1. テンプレートをコピーします。Reaperを起動し、コピーしたファイルを読み込みます。
2. 第二トラックに目的の音源をロードします。   
   ![001](https://github.com/reaperworker/loudness-velocity/assets/155607404/b22405fd-cf8d-4292-9954-f288fd84353f)
3. L+Rが第二チャンネルの出力となるようにします。   
   ![002](https://github.com/reaperworker/loudness-velocity/assets/155607404/782fad04-c6d0-4d39-af90-62ba1829bf84)
   ![003](https://github.com/reaperworker/loudness-velocity/assets/155607404/2b03db26-8c35-4961-8b9e-645a5d9e4608)
   ![004](https://github.com/reaperworker/loudness-velocity/assets/155607404/e0b0b1be-0077-4376-93db-9feb8c01996a)
4. 第三トラックのloudness_velocityの画面を表示しておきます。
   ![005](https://github.com/reaperworker/loudness-velocity/assets/155607404/51deae8c-577d-4621-9d3a-ff1a0944ea83)
   ![006](https://github.com/reaperworker/loudness-velocity/assets/155607404/85716f19-d52d-4b69-b86a-b065c86db8d2)
5. レンダリングのドライランを実行します。  
   [File]->[Render]   
   ![007](https://github.com/reaperworker/loudness-velocity/assets/155607404/2eb29092-17c7-440f-aba9-8bfd89b762c1)
   ![008](https://github.com/reaperworker/loudness-velocity/assets/155607404/4920c205-5147-4dc1-9960-bc41e08dfb4a) 
6. loudness_velocityの画面で測定結果を保存します。  
   ![009](https://github.com/reaperworker/loudness-velocity/assets/155607404/0af2beaf-34dc-4234-ab56-9d76db77cf51)
   ![010](https://github.com/reaperworker/loudness-velocity/assets/155607404/30d51669-74b9-4e67-a9a1-36f3d72cd89f)
7. 測定結果は次のファイルに保存されています。メモ帳で開きます。
   ```
   C:\Users\<someone>\AppData\Roaming\REAPER\presets\js-000_loudness_velocity.ini
   ```
8. 次の箇所が保存されたデータです。クリップボードにコピーします。  
   ![011](https://github.com/reaperworker/loudness-velocity/assets/155607404/dea22289-3fe6-458e-96b9-92f7908cd2d4)
9. decoder.xlsxを適当なファイルにコピーし、そのシートのセルB2にペーストします。  
   ![012](https://github.com/reaperworker/loudness-velocity/assets/155607404/492c4f6b-b3dc-4e83-8fc8-6992b245ebeb)
   C列がヴェロシティ、K列が測定結果、L列は最大値を0dBとした調整した値です。
