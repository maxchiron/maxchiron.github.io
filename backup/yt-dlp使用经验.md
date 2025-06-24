插件安装位置 plugin install location
windows: `C:\Users\Administrator\.config\yt-dlp\plugins`

下载并保存日志：
`yt-dlp -ciwv -R infinite -t sleep --cookies ..\yt-dlp_cookies.txt -o "shorts/%(release_date)s-%(id)s-%(title)s.%(ext)s" --extractor-args "youtubepot-bgutilhttp:base_url=http://127.0.0.1:4416" https://www.youtube.com/@cheerssports/shorts 2>&1 | Tee-Object -FilePath yt-dlp_log-shorts.log`