---
title: Olasılık Yoğunluk Fonksiyonu (PDF)
date: 2023-10-12 14:15:00 +0100
categories: [istatistik, veribilimi]
tags: [istatistik, veribilimi, makineogrenimi]
math: true
---

# Olasılık Yoğunluk Fonksiyonu ve Çekirdek Yoğunluk Tahmini

Bu yazıda sizlere _Probability Density Function_ (Olasılık Yoğunluk Fonksiyonu) konusunu ele alacağız.

Yazının devamında Olasılık Yoğunluk Fonksiyonu için **PDF** kısaltmasını kullanacağım.

#### Olasılık Yoğunluk Fonskiyonu (PDF), $[-\infty,+\infty]$ değer aralığına sahip bir rastgele değişkenin, alacağı değerin hangi aralıkta bulunacağı olasılığını hesaplamak için kullanılır.

Cümle biraz kafa karıştırıcı olmakla birlikte biraz daha matematiksel açıdan baktığımızda anlaşılırlığı ortaya çıkıyor.

Örneğin elimizde bir $X$ değişkeni olduğunu düşünelim. Bu değişken değer aralığı $[-100,100]$ olsun. Ancak $[-100,100]$ değer aralığı yalnızca tam sayılardan oluşmayan ve içerisinde sonsuz sayıda değer barındıran bir aralıktır. Bu sebepten bu aralık içerisinde $X$ değişkeni için _örneğin_ 10 değerinin ihtimalini hesaplamak basit olasılık hesabından karşımıza şu şekilde çıkacaktır.

$$P(x) = \frac{n}{N} = \frac{Beklenen Değer}{Toplam Değerler}$$

Bu senaryoda, $[-\infty,+\infty]$ değer aralığı içerisinde, örneğin 10 değerini elde etmek istediğimizde, tüm değerler arasında 10 değeri 1 adet olduğu için formül aşağıdaki şekilde olacaktır:

$$P(x) = \frac{1}{\infty} = 0$$

Yani sonsuz aralıkta bir değer aralığından, istenen değeri olasılıksal olarak elde etme sonucumuz daima sıfırdır. İşte bu noktada **PDF** bize, bu değerin hangi aralıkta olası olduğunu veren bir fonksiyon olarak görev yapar. Biz $10$ değerinin bu sonsuz aralıktaki ihtimalini hesaplamak istediğimizde, başvurmamız gereken şey bu değerin hangi iki değer aralığında olduğunu bulmaya çalışmak olacaktır.

İşte bu hususta, PDF bizlere şu formülü vermektedir.

$$
P(a \leq X \leq b) = \int_{a}^{b} f_X(x) \, dx
$$

### Olasılık Yoğunluk Fonksiyonu (PDF) Tanımı

$$
f_X(x) = \lim_{{\Delta x \to 0}} \frac{P(x \leq X < x + \Delta x)}{\Delta x}
$$

$f_X(x)$ , $X$ rastgele değişkeninin belirli bir $x$'e yakın değerini alma olasılığını verir. Ancak bu noktada önemli olan bir diğer konu, fonksiyonun genellikle veri setinin istatistiksel dağılımlarına göre belirleniyor olmasıdır. $f_X(x)$ fonksiyonu, $X$ değişkeninin olasılık dağılımını tanımlar ve bu dağılım, $X$ değişkeninin alabileceği tüm değerler üzerinden entegre edildiğinde 1'e eşittir:

$$
\int_{-\infty}^{+\infty} f_X(x) \, dx = 1
$$

### Örnek: Normal Dağılım

Normal dağılım, yaygın olarak kullanılan bir olasılık dağılımıdır ve şu PDF ile tanımlanır:

$$
f_X(x) = \frac{1}{\sqrt{2\pi}\sigma} e^{ -\frac{(x-\mu)^2}{2\sigma^2} }
$$

Burada $(\mu$\) ortalamayı ve \($\sigma$\) standart sapmayı temsil eder.

#### Örnek Soru

Bir rastgele değişken $(X)$, $(\mu = 0)$ ve \($\sigma = 1$\)parametrelerine sahip standart normal dağılıma sahiptir. $(P(-1 \leq X \leq 1))$ olasılığını bulalım.

#### Çözüm

Bu soruyu çözmek için yukarıda verilen formülü kullanacağız:

$$
P(-1 \leq X \leq 1) = \int_{-1}^{1} f_X(x) \, dx
$$

$$
= \int_{-1}^{1} \frac{1}{\sqrt{2\pi}\cdot1} e^{ -\frac{(x-0)^2}{2\cdot1^2} } \, dx
$$

Bu integrali çözmek için matematiksel yöntemler veya sayısal integrasyon yöntemleri kullanılabilir. Ancak, standart normal dağılım tabloları veya bilgisayar yazılımları ile bu olasılık doğrudan bulunabilir ve yaklaşık olarak 0.6827 olduğunu göreceksiniz.

Bunu da Python örneği ile tamamlayalım:

```python
import scipy.stats as stats

# Parametreler
mu = 0  # Ortalama
sigma = 1  # Standart sapma

# Olasılığı hesapla
p = stats.norm.cdf(1, mu, sigma) - stats.norm.cdf(-1, mu, sigma)

print(f"P(-1 <= X <= 1) = {p:.4f}")
```

Bu Python kodu, $(-1 \leq X \leq 1)$ aralığındaki olasılığı hesaplamak için SciPy kütüphanesinin `norm.cdf` fonksiyonunu kullanır. `norm.cdf` fonksiyonu, normal dağılımın kümülatif dağılım fonksiyonunu (CDF) hesaplar. Yukarıdaki kodda, $(P(-1 \leq X \leq 1))$ olasılığını hesaplamak için 1 ve -1 noktalarındaki CDF değerleri arasındaki farkı alırız. Çıktı olarak bu olasılığı 4 ondalık basamak doğrulukla ekrana yazdırırız.
