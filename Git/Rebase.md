# ๐ฅ Rebase ํ์ฉํด ์ปค๋ฐ ๋ ์ง ๋ณ๊ฒฝํ๊ธฐ


## 1. git add .

## 2. git commit -m "๋ฉ์ธ์ง"

```
์ฌ๊ธฐ์๋ถํฐ ์ง์ง
```

## 3. git log
* ๋ ์ง๋ฅผ ๋ณ๊ฒฝํ  ์ปค๋ฐ์ ์ด์  ์ปค๋ฐ hash๊ฐ์ ๋ณต์ฌํ๋ค.   


![image](https://user-images.githubusercontent.com/61656046/132023913-8cb34aa1-e859-4443-998f-62ac4b37e778.png)

## 4. git rebase [hash ๊ฐ] -i
![image](https://user-images.githubusercontent.com/61656046/132024494-09e9635d-e25a-413d-aea0-afd96daec88e.png)   
๊ทธ๋ฌ๋ฉด ํด๋น ์ปค๋ฐ ์ดํ์ ๋ชจ๋  ์ปค๋ฐ๋ค์ด ํธ์ง์ฐฝ์ ๋์ค๊ฒ ๋๋ค.

### 4-1. a ์๋ ฅ์ผ๋ก ํธ์ง๋ชจ๋ ์ ํ
![image](https://user-images.githubusercontent.com/61656046/132024950-e361876c-19ed-4a6d-9856-83995dbbfa36.png)
* a ๋ฅผ ์๋ ฅํ๋ฉด ๊ฐ์ฅ ๋ฐ์ **-- INSERT --** ๊ฐ ์๊ธฐ๋๋ฐ ์ด๋ ํธ์ง์ด ๊ฐ๋ฅํ๋ค.

### 4-2. edit ๋ก ๋ด์ฉ ๋ณ๊ฒฝ ํ esc ๋ฒํผ
![image](https://user-images.githubusercontent.com/61656046/132025173-3ed6e175-218d-47b8-b55f-b3762cfe135b.png)   
์์ ํ  ์ปค๋ฐ์ ์ ํ๋ด์ฉ์ edit ๋ก ์์ ํด์ค๋ค. ๊ทธ๋ฆฌ๊ณ  esc ๋ฒํผ์ผ๋ก ์์ ์ ๋ง์น๋ค.

### 4-3. :wq! ์๋ ฅ์ผ๋ก ๋ณ๊ฒฝ๋ด์ฉ ์ ์ฉ

![image](https://user-images.githubusercontent.com/61656046/132025476-d8c6d376-8709-465c-8030-8b5c5274daab.png)   
* ๊ทธ๋ฌ๋ฉด ๋ธ๋์น๋ช ์์ REBASE๋ผ๊ณ  ์๋ ฅ๋ ๊ฒ์ ๋ณผ ์ ์๋ค.

## 5. ๋ณ๊ฒฝํ  ๋ ์ง ๋ช๋ น์ด ์๋ ฅ
```
GIT_COMMITTER_DATE="{๋ณ๊ฒฝํ ๋ ์ง}" git commit --amend --no-edit --date "{๋ณ๊ฒฝํ ๋ ์ง}"

// ์์ (21.08.16, 10:00:00)
GIT_COMMITTER_DATE="Aug 16 10:00:00 2021 +0900" git commit --amend --no-edit --date "Aug 16 10:00:00 2021 +0900"
```   
![image](https://user-images.githubusercontent.com/61656046/132026661-4f92325b-2ccf-49da-a88d-766b0eb03538.png)   
## 6. git rebase --continue ์๋ ฅ์ผ๋ก ๋ณ๊ฒฝ์ฌํญ ์ ์ฉ
![image](https://user-images.githubusercontent.com/61656046/132026760-b918fe56-4f5b-4e5c-acc4-fba2ec65a767.png)   
* ์ ์ฉ์ด ๋๋๋ฉด ๋ธ๋์น ์์ ์๋ REBASE ๋ฌธ์๊ฐ ์ฌ๋ผ์ง๋ค.

## 7. git log ๋ฅผ ํตํด ํ์ธ ๋ฐ push
![image](https://user-images.githubusercontent.com/61656046/132027428-ffbd4258-d6a4-4d34-994c-5c377ea712b5.png)   
* git log ์์ ๋ ์ง๊ฐ ๋ณ๊ฒฝ ๋ ๊ฒ์ ํ์ธ ํ  ์ ์๋ค. ๋.









