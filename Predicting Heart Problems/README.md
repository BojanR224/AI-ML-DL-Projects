**Податочно множество**

![image](https://user-images.githubusercontent.com/61628838/206916842-ee69587a-7425-48d1-b3e8-45184c75f1d1.png)

 
•	Chest pain (CP):  Вредности од 0 до 3

•	Trestbps: крвен притисок во одморена состојба

•	Chol: холестерол во mg/dl

•	Fbs: дали има >120 mg/dl шеќер во крв

•	Restecg: резултати од електрокардиографија

•	Thalach: максимален пулс

•	Exang: Болка во гради од вежбање

•	Oldpeak: ST depression иницирано од вежбање

•	Ca: број на главни аорти

•	Thal: дефект на аорти

•	Target: Дали пациентот има срцеви заболувања?

**Зависности помеѓу атрибутите**
 ![image](https://user-images.githubusercontent.com/61628838/206916874-d35066c5-31c0-47aa-a352-287afbd8a82a.png)

**Визуелизација со PCA**
![image](https://user-images.githubusercontent.com/61628838/206916880-3ba59299-ac46-46e3-a39f-afbc6354c123.png)


**Отстранување на outliers**
![image](https://user-images.githubusercontent.com/61628838/206916885-17317a8d-8654-44a8-a24b-77955fdbecac.png)

 => Отстранети се 16 редици од множеството, така што мерката употребена за отфрлање на редици е ако некој атрибут има вредност поголема од  3 * Standard deviation на соодветниот атрибут

**Missing values**
![image](https://user-images.githubusercontent.com/61628838/206916888-23f7b175-fed6-41ed-9c23-8b0492c386d8.png)




**Дрво на одлучување**
![image](https://user-images.githubusercontent.com/61628838/206916898-091e5250-5476-470d-a23c-524d994a328c.png)
![image](https://user-images.githubusercontent.com/61628838/206916905-efce6a82-f533-44cd-8b43-cde3f350db5b.png)

  
	Споредба на модели со различна вредност на cpp_alphas и тунирање на истите 
![image](https://user-images.githubusercontent.com/61628838/206916913-ceb3b153-3deb-4ba1-bc5d-289e167bc0d2.png)

**Random forest classifier**
![image](https://user-images.githubusercontent.com/61628838/206916939-7db8969a-fe32-4fe0-94b8-cceb7dd1f2aa.png)

=> Најдобриот модел е со max depth = 12, со тоа се достигнува вредност на test accuracy со над 0.86
**GaussianNB**
![image](https://user-images.githubusercontent.com/61628838/206916954-9c8ca4af-9c35-4e5d-a873-4f4124a72550.png)

**CategoricalNB**
Промена на атрибутите од непрекинат тип според следниве правила и отстранување на атрибутот oldpeak бидејќи има голема зависност со slope атрибутот:
•	chol: <150 (normal), >150 <200 (mildly high), >200 <500 (high), >500 (very high)

•	age: 18-39 (adult), 40-59 (middle aged), >60 (senior adult)

•	trestbps (Resting blood pressure, Systolic): <120 (normal), >120 <140 (elevated), >140 <160 (High blood pressure), >160 (Hypertension)

•	thalach (Maximum hearth rate): <120 normal, >120 <150 moderate, >150 high

•	oldpeak: removed

Се добиваат следниве резултати каде што има мало подобрување во accuracy:
![image](https://user-images.githubusercontent.com/61628838/206916964-0493f8ba-066d-4ea7-ab2d-901a09092596.png)

**K-Neighbors Classifier**
![image](https://user-images.githubusercontent.com/61628838/206916977-9bacd6ae-00c5-4fcc-a77a-5ae19e7e3d2e.png)

=>	Тестирање на различни модели, така што за секоја К вредност употребени се 100 различни варијанти на множество за да биде појасно кој е најдобрата вредност на К
Со одбирање на к=10 и користење на Minkowski мерка за дистанца (p=1) се добиваат следниве резултати
![image](https://user-images.githubusercontent.com/61628838/206916981-a611eed2-02da-4070-8baa-3c8f779decc5.png)


**Предвидување на холестерол во крвта со помош на линеарна регресија**

Резултати на обична линеарна регресија:
![image](https://user-images.githubusercontent.com/61628838/206916994-122fa9fc-1e86-4fdf-b2b5-d89441ffa569.png)

Резултати на обична линеарна регресија со скалирање на променливите:
![image](https://user-images.githubusercontent.com/61628838/206916999-c8117613-022e-415e-af0e-71107d6d5a8b.png)

Полиномна регресија со скалирање:
![image](https://user-images.githubusercontent.com/61628838/206916989-2bd9802a-3252-47b4-a8af-9c1ea84f65f7.png)

**Ridge регресија**
 ![image](https://user-images.githubusercontent.com/61628838/206917007-266c5ef7-3c65-4e5a-b5c7-feafe0ed71d5.png)



**Предвидување на target атрибутот со помош на логистичка регресија**
![image](https://user-images.githubusercontent.com/61628838/206917012-94b96d74-0358-4e40-86ab-a9a7d39b62bf.png)
![image](https://user-images.githubusercontent.com/61628838/206917021-a71dfa84-6cf0-4845-8f2e-fa274183c28b.png)

**LDA со не балансирано и балансирано множество**
![image](https://user-images.githubusercontent.com/61628838/206917059-19ee21cb-cf66-4bd2-95dd-5c6dd1b060de.png)

  
**Не балансирано**
![image](https://user-images.githubusercontent.com/61628838/206917074-e13b868f-f534-4ea0-affe-414d69de5f66.png)

**Балансирано**
![image](https://user-images.githubusercontent.com/61628838/206917080-81bf639d-c893-4aa5-bbdb-7af90e037a63.png)
    
    
**Ensemble методи**

Со помош на 3 различни модели (Логистички регресионен модел, Random forest classifier и KNeighborsClassifier) се добива Test Accuracy:
![image](https://user-images.githubusercontent.com/61628838/206917090-ad96702d-a389-4dde-b9c0-01da0d0bae24.png)

**Кластер модели**

**КMeans**
![image](https://user-images.githubusercontent.com/61628838/206917101-c9df238e-8ee8-45a8-9471-d62384a258f4.png)
 
**Algomerative кластерирање**
![image](https://user-images.githubusercontent.com/61628838/206917108-1f282d52-47c8-4c34-bc41-197308e9a078.png)

