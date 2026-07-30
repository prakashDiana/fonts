```

ffmpeg -i input.mp4 -filter_complex \
"[0:v]setpts=PTS[tl]; \
 [0:v]setpts=0.5*PTS[tr]; \
 [0:v]setpts=0.746*PTS[bl]; \
 [0:v]setpts=2.0*PTS[br]; \
 [tl][tr][bl][br]xstack=inputs=4:layout=0_0|w0_0|0_h0|w0_h0[v]; \
 [0:a]asetpts=PTS[atl]; \
 [0:a]atempo=2.0[atr]; \
 [0:a]atempo=1.34[abl]; \
 [0:a]atempo=0.5[abr]; \
 [atl][atr][abl][abr]amix=inputs=4:duration=shortest[a]" \
-map "[v]" -map "[a]" -c:v libx264 -crf 18 -pix_fmt yuv420p -c:a aac -b:a 192k output_with_audio.mp4


```
