# Meloncrawling
크롤링하는 법(멜론/ 출처: https://www.youtube.com/watch?v=rtm53GP62ss) import requests from bs4 import BeautifulSoup

browser = webdriver.Chrome('C:/Users/82104/project1/chromedriver.exe') browser.get(불러올 주소)

html = browser.page_source soup = BeautifulSoup(html, 'html.parser')

-원하는 정보 찾기 soup.select() -태그 1개 정보 알려주기 soup.select('태그명') soup.select('.class속성값') (#id속성값) / (태그명.class속성값) -태그 구조를 이용 soup.select('상위태그정보> 하위태그정보') soup.select('더상위태그정보>상위태그정보>하위태그정보')

원하는정보 찾기

노래정보뭉치 / 덩어리 먼저찾기 --> 100개 노래1곡 정보 뭉치/덩어리 --> 내가 원하는 정보 찾기 원하는 값은 100개 song_list = soup.select('tr') len(song_list) ... 101개

song_list = soup.select('tbody>tr') 상위값으로 올려서 len(song_list) ... 100개

song = song_list[0]

soup.select() # soup 데이터 내에서 찾기 -> 페이지 전체 html song.select() #song 데이터 찾기 -> 1곡 정보에서만 찾기

title = song.select('a') #결과: 6

title = song.select('span > a') #결과: 2

title = song.select('div>span>a') #결과: 2

title = song.select('div.ellipsis rank01>span>a') #결과: 0

title = song.select('div.ellipsis.rank01>span>a') #결과: 리스트형태

title = song.select('div.ellipsis.rank01>span>a')[0] #결과: 태그 선택

title = song.select('div.ellipsis.rank01>span>a')[0].text #결과: 화면에 보이는 글

top100순으로 노래제목 출력하는 for문 song = song_list[0] for song in song_list: title = song.select('div.ellipsis.rank01>span>a')[0].text print(title)
