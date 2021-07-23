# PROJECT 01

💡영화의 정보가 정리된 json 데이터 파일을 이용한 첫 프로젝트💡

> Goal of the Project01
>
> - python 기본 문법 실습
> - 파일 입출력에 대한 이해
> - 데이터 구조에 대한 분석과 이해
> - 데이터를 가공하고 JSON 형태로 저장



## A. 원하는 정보 추출

주어진 하나의 샘플 영화 데이터에서 원하는 정보만을 뽑아 dictionary 형태로 반환하는 함수를 만든다. 제공된 데이터 중 id, title, poster_path, vote_average, overview, genre_ids 키에 해당되는 정보만을 갖고 오도록 설계했다.

```python
def movie_info(movie):
    info_dict = {}
    for info in movie:
        info_dict['id'] = movie['id']
        info_dict['title'] = movie['title']
        info_dict['poster_path'] = movie['poster_path']
        info_dict['vote_average'] = movie['vote_average']
        info_dict['overview'] = movie['overview']
        info_dict['genre_ids'] = movie['genre_ids']

    return info_dict
```

함수에 넣는 `movie` 에는 주어진 샘플 데이터 파일이 들어간다. 이 데이터 파일은 딕셔너리의 형태로 만들어져 있다. 이 딕셔너리 파일을 for문을 통해 한바퀴 돌아주면서 원하는 key값이 있을 때마다 새로 만든 `info_dict` 에 key와 value의 값을 저장하도록 했다. 그리고 마지막으로 `info_dict ` 를 반환한다.

이렇게 만들어진 함수의 결과는 다음과 같다.

```python
# 저장된 json 파일 불러오기
movie_json = open('data/movie.json', encoding='UTF8')
movie_dict = json.load(movie_json)

pprint(movie_info(movie_dict))
```

**Output:**

```
{'genre_ids': [18, 80],
 'id': 278,
 'overview': '촉망받는 은행 간부 앤디 듀프레인은 아내와 그녀의 정부를 살해했다는 누명을 쓴다. 주변의 증언과 살해 현장의 '
             '그럴듯한 증거들로 그는 종신형을 선고받고 악질범들만 수용한다는 지옥같은 교도소 쇼생크로 향한다. 인간 말종 '
             '쓰레기들만 모인 그곳에서 그는 이루 말할 수 없는 억압과 짐승보다 못한 취급을 당한다. 그러던 어느 날, 간수의 '
             '세금을 면제받게 해 준 덕분에 그는 일약 교도소의 비공식 회계사로 일하게 된다. 그 와중에 교도소 소장은 죄수들을 '
             '이리저리 부리면서 검은 돈을 긁어 모으고 앤디는 이 돈을 세탁하여 불려주면서 그의 돈을 관리하는데...',
 'poster_path': '/3hO6DIGRBaJQj2NLEYBMwpcz88D.jpg',
 'title': '쇼생크 탈출',
 'vote_average': 8.7}
```

원하는 6가지의 정보가 제대로 저장이 되어 출력되고 있음을 보여준다.



## B. genre_ids → genre_names

A에서 원하는 정보만을 추출했다면, 이번에는 장르의 id를 숫자에서 이름으로 바꾸어주는 과정이다. 함수를 호출해서 쓰고 싶었으나, problem_a, b, c의 함수 이름이 전부 똑같이 써있어서 나중에 헷갈릴 수 있으므로 아까 작성했던 코드를 그대로 복사해와서 이용하기로 했다.

```python
def movie_info(movie, genres):
    info_dict = {}
    # 원하는 정보만 추출
    for info in movie:
        info_dict['id'] = movie['id']
        info_dict['title'] = movie['title']
        info_dict['poster_path'] = movie['poster_path']
        info_dict['vote_average'] = movie['vote_average']
        info_dict['overview'] = movie['overview']
        info_dict['genre_ids'] = movie['genre_ids']
    
    # genre_ids -> genre_names
    genre_list = info_dict['genre_ids']
    for i in range(len(genre_list)):
        for dict in genres:
            if dict['id'] == genre_list[i]:
                genre_list[i] = dict['name']
                break
    info_dict['genre_names'] = info_dict.pop('genre_ids')
    return info_dict 
```

이번에는 `movie_info` 함수가 영화 정보와 장르 정보 두가지를 받는다. 

영화 정보`movie`는 역시나 dictionary의 형태로 들어오고 장르 정보`genres`는 list의 형태로 들어온다. `genres`는 id, name으로 구성된 dictionary를 여러개 포함하고 있는 list이므로 전체 리스트를 돌면서 원하는 id의 값을 찾아주기로 했다. 영화의 정보를 받는 `movie`는 아까 말했듯이 dictionary 형태이고 이 중 `genre_ids` 부분을 찾아주어야 하는데 `genre_ids`가 list로 이루어져 있었기 때문에 `genre_ids`의 list 역시 한바퀴 돌아야 한다. 결과적으로 for문을 두번 쓰게 된 셈이다.

```python
genre_list = info_dict['genre_ids']
for i in range(len(genre_list)):
    for dict in genres:
```

for문을 돌면서 원하는 id 값을 발견하면 `info_dict`의 `genre_ids` 안의 list의 요소들을, 숫자에서 장르 이름으로 바꾸어 주었다. 만약 숫자에서 이름으로 바뀌었다면 더이상 두번째 for문 `for dict in genres`을 돌 필요성이 사라지므로 조금이라도 시간을 단축해주기 위해 break로 빠져나온 뒤, 그 다음 장르 넘버를 이름으로 바꾸어주는 for문 `for i in range(len(genre_list))`을 다시 돌게 만들었다.

`info_dict`에서 `genre_ids`의 value값을 모두 숫자에서 이름으로 바꾸어 주었으면 이제 key값을 바꾸어 줄 차례이다. 새롭게 `genre_names`라는 key의 이름을 설정하고 난 후 `genre_ids`의 값을 뽑아서 저장한 뒤 `genre_names`에 넣어주었다. 이 함수를 실행시키면 그 결과는 다음과 같다.

```python
movie_json = open('data/movie.json', encoding='UTF8')
movie = json.load(movie_json)

genres_json = open('data/genres.json', encoding='UTF8')
genres_list = json.load(genres_json)
pprint(movie_info(movie, genres_list))
```

**Output:**

```
{'genre_names': ['Drama', 'Crime'],
 'id': 278,
 'overview': '촉망받는 은행 간부 앤디 듀프레인은 아내와 그녀의 정부를 살해했다는 누명을 쓴다. 주변의 증언과 살해 현장의 '
             '그럴듯한 증거들로 그는 종신형을 선고받고 악질범들만 수용한다는 지옥같은 교도소 쇼생크로 향한다. 인간 말종 '
             '쓰레기들만 모인 그곳에서 그는 이루 말할 수 없는 억압과 짐승보다 못한 취급을 당한다. 그러던 어느 날, 간수의 '
             '세금을 면제받게 해 준 덕분에 그는 일약 교도소의 비공식 회계사로 일하게 된다. 그 와중에 교도소 소장은 죄수들을 '
             '이리저리 부리면서 검은 돈을 긁어 모으고 앤디는 이 돈을 세탁하여 불려주면서 그의 돈을 관리하는데...',
 'poster_path': '/3hO6DIGRBaJQj2NLEYBMwpcz88D.jpg',
 'title': '쇼생크 탈출',
 'vote_average': 8.7}
```

`genre_ids`에서 `genre_names`로 정확하게 바뀐 것을 확인할 수 있다.



## C. 다중 데이터 분석 및 수정

이번엔 여러개의 영화 데이터를 한번에 분석하고 수정하는 과정이다. 20개의 영화 데이터가 주어지고 이 데이터들에서 원하는 정보만을 추출하는 함수를 작성할 것이다.

```python
def movie_info(movies, genres):
    for i in range(len(movies)):
        movie = movies[i]
        info_dict = {}
        # 원하는 정보만 추출
        for info in movie:
            info_dict['id'] = movie['id']
            info_dict['title'] = movie['title']
            info_dict['poster_path'] = movie['poster_path']
            info_dict['vote_average'] = movie['vote_average']
            info_dict['overview'] = movie['overview']
            info_dict['genre_ids'] = movie['genre_ids']
        
        # genre_ids -> genre_names
        genre_listed = info_dict['genre_ids']
        for id_num in range(len(genre_listed)):
            for dict in genres:
                if dict['id'] == genre_listed[id_num]:
                    genre_listed[id_num] = dict['name']
                    break
        info_dict['genre_names'] = info_dict.pop('genre_ids')
        movies[i] = info_dict
    return movies  
```

최종 완성된 `movie_info`함수에서는 `movies`에서 여러개의 영화정보를 list로 받고, `genres`는 아까와 똑같은 데이터로 list로 받는다. A, B에서 작성한 함수를 이용해 주었기 때문에 전체적인 구성은 비슷하다. 

이번 함수는 20개의 데이터를 받아주므로, for문을 이용해서 `movies` 안의 영화 정보를 하나하나 확인해주었다. list 안에는 dictionary형태로 정보가 저장되어 있고 list의 요소에만 접근한다면 그 뒤는 지난 함수와 똑같이 진행된다. 따라서 `movie = movies[i]` 를 통해 for문을 돌면서 `movies` 안의 영화 정보를 하나씩 꺼내 `movie`에 넣어준 뒤 지난 수순에서 했던 것처럼 원하는 정보만 추출하고 장르 숫자를 이름으로 바꾸는 과정을 진행했다. 이렇게 만들어진 `info_dict`은 다시 `movies[i]`에 넣어주어 list의 값이 확실하게 바뀔 수 있도록 했다.

함수의 결과는 다음과 같다:

```python
movies_json = open('data/movies.json', encoding='UTF8')
movies_list = json.load(movies_json)

genres_json = open('data/genres.json', encoding='UTF8')
genres_list = json.load(genres_json)
pprint(movie_info(movies_list, genres_list))
```

**Output:**

```
[{'genre_names': ['Drama', 'Crime'],
  'id': 278,
  'overview': '촉망받는 은행 간부 앤디 듀프레인은 아내와 그녀의 정부를 살해했다는 누명을 쓴다. 주변의 증언과 살해 현장의 '
              '그럴듯한 증거들로 그는 종신형을 선고받고 악질범들만 수용한다는 지옥같은 교도소 쇼생크로 향한다. 인간 말종 '
              '쓰레기들만 모인 그곳에서 그는 이루 말할 수 없는 억압과 짐승보다 못한 취급을 당한다. 그러던 어느 날, 간수의 '
              '세금을 면제받게 해 준 덕분에 그는 일약 교도소의 비공식 회계사로 일하게 된다. 그 와중에 교도소 소장은 죄수들을 '
              '이리저리 부리면서 검은 돈을 긁어 모으고 앤디는 이 돈을 세탁하여 불려주면서 그의 돈을 관리하는데...',
  'poster_path': '/3hO6DIGRBaJQj2NLEYBMwpcz88D.jpg',
  'title': '쇼생크 탈출',
  'vote_average': 8.7},
 
 ...
 
 {'genre_names': ['Romance', 'Animation', 'Drama'],
  'id': 372058,
  'overview': '시골에 사는 소녀 미츠하(가미시라이시 모네)는 어느 날 잠에서 깬 후 자신의 몸이 남자로 바뀐 걸 알게 된다. '
              '같은 시간, 도쿄에 사는 소년 타키(가미키 류노스케) 역시 이 기이한 상황을 겪고 있다. 낯선 가족, 낯선 '
              '친구들, 낯선 풍경들... 서로에게 이어진 끈을 알게 된 둘은 둘만의 규칙을 정하고 점차 상황을 받아들이기 '
              '시작한다. 서로에게 남긴 메모를 확인하며  점점 친구가 되어가는 타키와 미츠하. 언제부턴가 더 이상 몸이 바뀌지 '
              '않자  자신들이 특별하게 이어져있었음을 깨달은  타키는 미츠하를 만나러 가는데...',
  'poster_path': '/wx1Dxr4UyvN18SyC5GsVWWWtYja.jpg',
  'title': '너의 이름은',
  'vote_average': 8.6},
 {'genre_names': ['Animation', 'Comedy', 'Romance', 'Drama', 'Fantasy'],
  'id': 572154,
  'overview': '하늘과 바다가 반짝이는 마을 "후지사와"에 사는 고등학생 아즈사가와 사쿠타는 같은 학교 선배이자 연인인 사쿠라지마 '
              '마이와 설레는 일상을 보내고 있다. 하지만 어느 날 첫사랑인 마키노하라 쇼코가 등장하면서 그 일상은 완전히 '
              "뒤바뀌어 버린다. 알 수 없는 이유로 '중학생'과 '어른', 두 명이 존재하는 쇼코와 부득이한 동거를 하면서 "
              "사쿠타와 마이의 관계가 삐걱거리기 시작한다. 그러던 중 '중학생 쇼코'가 위중한 병을 앓고 있다는 것을 알고 "
              '사쿠타의 가슴 흉터는 다시 벌어지는데...',
  'poster_path': '/hqNkm15rQI6049Pg3XPSE8PMW98.jpg',
  'title': '청춘 돼지는 꿈꾸는 소녀의 꿈을 꾸지 않는다',
  'vote_average': 8.6},
 {'genre_names': ['Animation', 'Family', 'Fantasy'],
  'id': 129,
  'overview': '평범한 열 살 짜리 소녀 치히로 식구는 이사 가던 중 길을 잘못 들어 낡은 터널을 지나가게 된다. 터널 저편엔 '
              '폐허가 된 놀이공원이 있었고 그곳엔 이상한 기운이 흘렀다. 인기척 하나 없는 이 마을의 낯선 분위기에 불길한 '
              '기운을 느낀 치히로는 부모님에게 돌아가자고 조르지만 부모님은 호기심에 들떠 마을 곳곳을 돌아다니기 시작한다. 어느 '
              '음식점에 도착한 치히로의 부모님은 그 곳에 차려진 음식들을 보고 즐거워하며 허겁지겁 먹어대다가 돼지로 변해버린다. '
              '겁에 질려 당황하는 치히로에게 낯선 소년 하쿠가 나타나 빨리 이곳을 나가라고 소리치는데...',
  'poster_path': '/u1L4qxIu5sC2P082uMHYt7Ifvnj.jpg',
  'title': '센과 치히로의 행방불명',
  'vote_average': 8.5},
  
 ...
 
 {'genre_names': ['Action',
                  'Adventure',
                  'Animation',
                  'Science Fiction',
                  'Comedy'],
  'id': 324857,
  'overview': '평범한 10대 마일스 모랄레스는 우연히 방사능 거미에 물려 스파이더맨 능력을 가지게 된다. 혼란스러워하던 마일스는 '
              '악당과 싸우고 있는 피터 파커를 마주치게 되고 피터 파커는 마일스가 자신과 같은 능력을 가지고 있음을 직감한다. '
              '여러 개의 평행세계가 존재한다는 것을 알게 된 마일스와 피터 파커는 이후 스파이더우먼 스파이더 그웬, 스파이더맨 '
              '누아르, 스파이더햄 등 평행세계 속 공존하는 모든 스파이더맨들을 만나게 되는데... 하나의 유니버스에서 만나 팀을 '
              '결성한 스파이더맨들은 과연 세계를 구할 수 있을까?',
  'poster_path': '/vnWgIIEWAvWKOI65tm6h6VRbyY8.jpg',
  'title': '스파이더맨: 뉴 유니버스',
  'vote_average': 8.4},
 {'genre_names': ['Fantasy', 'Animation', 'Adventure'],
  'id': 4935,
  'overview': '19세기 말 마법과 과학이 공존하고 있는 세계 앵거리. 소피는 돌아가신 아버지의 모자상점에서 쉴틈없이 일하는 '
              '18살 소녀이다. 어느 날 오랫만에 마을로 나간 소피는 우연히 하울을 만나게 된다. 하울은 왕실 마법사로서 '
              '핸섬하지만 조금 겁이 많은 청년이다. 황무지 마녀는 두 사람의 사이를 오해, 주문을 걸어 소피를 90살의 늙은 '
              '할머니로 만들어 버린다. 가족을 걱정한 소피는 집을 나오게 되고 황무지를 헤매다가 하울이 사는 성에서 가정부로 '
              '낯선 생활을 시작한다. 4개의 다리로 걷는 기괴한 움직이는 성 안에서 하울과 소피의 기묘한 사랑과 모험이 '
              '시작되는데...',
  'poster_path': '/xiz6TiSduvR1U3VLfWVlBEdT9fO.jpg',
  'title': '하울의 움직이는 성',
  'vote_average': 8.4},
 {'genre_names': ['Comedy'],
  'id': 914,
  'overview': '세계대전에서 패배한 토매니아국에 힌켈이라는 독재자가 나타나 악명을 떨친다. 한편, 힌켈과 닮은꼴 외모의 이발사 '
              '찰리는 국가의 유태인 탄압정책으로 인해 곤경에 처하지만 병사로 참전했던 전쟁에서 우연히 구해줬던 슐츠 장교의 '
              '도움을 받아 위기를 모면한다. 독재자 힌켈의 악행은 갈수록 도를 더해가고, 찰리는 유태인 수용소에 끌려가게 되지만 '
              '기지를 부려 탈옥에 성공한다. 하지만 이발사와 똑같은 얼굴을 한 힌켈이 탈옥범으로 오해 받아 감옥에 잡혀 들어가게 '
              '되는데…',
  'poster_path': '/uw26mSTaA10hg2yuQfNaFLSeY3h.jpg',
  'title': '위대한 독재자',
  'vote_average': 8.4}]
```

결과는 너무 길어 중간 부분을 잘라주었다. 하나의 리스트 안에 20개의 영화가 dictionary의 형태로 정보를 나타내고 있으며, 원하는 정보만 추출되었고 `genri_ids` 역시 `genre_names`로 제대로 바뀐 것을 확인 할 수 있다. 



## D. 최고 수익 영화 찾기

세부적인 영화 정보는 data의 movie 폴더 안에 json 파일로 정리되어있다. json 파일 이름을 영화의 id로 구성되어 있다. 이 파일 안에서 영화의 수익 정보를 확인할 수 있는데 가장 수익이 높은 영화가 무엇인지 알아볼 수 있는 함수를 구성해보려고 한다.

```python
def max_revenue(movies):
    rev_dict = {}
    for i in range(len(movies)):
        movie_id = movies[i]['id'] 
        title = movies[i]['title']
        detailed_json = open('data/movies/'+ str(movie_id) +'.json', encoding='UTF8')
        detailed_info = json.load(detailed_json)
        revenue = detailed_info['revenue']
        rev_dict[title] = revenue

        max_rev = max(rev_dict, key=rev_dict.get)
    return max_rev
```

수익 정보는 영화 세부 정보에 있고 이를 불러오기 위해서는 영화의 id 를 알아야 하므로 `movies` 의 list 요소에 접근한 뒤 그 안의 dictionary에서  id 정보를 불러온다. id 값은 `movie_id` 에 저장하고 출력해줄 영화의 제목 정보는 `title` 에 저장했다. 그리고 `movie_id` 를 이용해 원하는 영화의 세부정보 파일을 불러오고 읽어준 뒤 그 안에서 revenue값을 뽑아 revenue에 저장해주었다.

`movies` 안에는 여러개의 영화 데이터가 있으므로 이 영화들의 수익정보만을 저장하는 dictionary인 `rev_dict` 을 새롭게 생성해주고 이 안에 key값을 `title` , value값을 `revenue` 로 입력해 주었다. 이후 value값의 max를 구하고 그 key값을 반환해주어 `max_rev` 에 저장한 뒤 함수에서 이 값을 return한다. 이렇게 작성된 함수의 결과는 다음과 같다.

```python
movies_json = open('data/movies.json', encoding='UTF8')
movies_list = json.load(movies_json)

print(max_revenue(movies_list))
```

**Output:**

```
반지의 제왕: 왕의 귀환
```

주어진 영화 데이터에서 가장 수익이 높았던 영화는 `반지의 제왕: 왕의 귀한` 이라는 사실을 확인할 수 있었다.



## E. 12월에 개봉한 영화 찾기

이번에도 역시 영화의 세부 정도 파일을 이용한다. 데이터 중 개봉일 정보를 불러와서 12월에 개봉한 영화를 리스트로 출력하는 함수를 구성해 보았다.

```python
def dec_movies(movies):
    dec_list = []
    for i in range(len(movies)):
        movie_id = movies[i]['id'] 
        title = movies[i]['title']
        detailed_json = open('data/movies/'+ str(movie_id) +'.json', encoding='UTF8')
        detailed_info = json.load(detailed_json)
        release_date = detailed_info['release_date']
        month = release_date.split('-')[1]
        if month == '12':
            dec_list.append(title)
    return dec_list
```

`movies` 로 받아온 데이터를 이용해 영화의 id, 제목의 정보를 추출하고 json 파일을 불러오는 것까지는 D에서 작성한 함수와 동일하다. 

이번에는 수익 정보가 아닌 개봉일 정보를 `release_date` 에 저장했다. 개봉일 정보는 년 - 월 - 일 순으로 작성되어 있었는데 현재 필요한 것은 '월'에 해당하는 정보이므로 이 문자열을 `-` 을 기준으로 split 해준 뒤 두번째 값만 `month` 에 저장해 주기로 한다. 

만약 `month` 의 값이 12라면 12월에 개봉한 영화이므로 이 영화의 제목을 `dec_list` 에 append 해준 뒤 전체 for 문을 다 돌고나서 작성된 `dec_list` 를 반환해준다. 

이렇게 작성된 함수의 결과는 다음과 같다.

```python
movies_json = open('data/movies.json', encoding='UTF8')
movies_list = json.load(movies_json)

print(dec_movies(movies_list))
```

**Output:**

```
['그린 마일', '인생은 아름다워', '반지의 제왕: 왕의 귀환', '스파이더맨: 뉴 유니버스']
```

