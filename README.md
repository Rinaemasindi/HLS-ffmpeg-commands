# HLS-ffmpeg-commands

## Create each video variant format
ffmpeg -i input.mp4 -vf scale=854:480 output_480p.mp4\
ffmpeg -i input.mp4 -vf scale=1280:720 output_720p.mp4\
ffmpeg -i input.mp4 -vf scale=1920:1080 output_1080p.mp4\

## Convert mp4 to hls supported format
ffmpeg -i output_480p.mp4 -codec: copy -start_number 0 -hls_time 10 -hls_list_size 0 -f hls output_480p.m3u8\
ffmpeg -i output_720p.mp4 -codec: copy -start_number 0 -hls_time 10 -hls_list_size 0 -f hls output_720p.m3u8\
ffmpeg -i output_1080p.mp4 -codec: copy -start_number 0 -hls_time 10 -hls_list_size 0 -f hls output_1080p.m3u8\

## Master m3u8 file

#EXTM3U\
#EXT-X-VERSION:3

#EXT-X-STREAM-INF:BANDWIDTH=800000,RESOLUTION=854x480\
output_480p.m3u8

#EXT-X-STREAM-INF:BANDWIDTH=1500000,RESOLUTION=1280x720\
output_720p.m3u8

#EXT-X-STREAM-INF:BANDWIDTH=2500000,RESOLUTION=1920x1080\
output_1080p.m3u8
