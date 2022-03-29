Die Notebooks in diesem Ordner beschäftigen sich mit StyleGAN2 und seinen Eigenschaften. [StyleGAN2](https://github.com/NVlabs/stylegan2)/[StyleGAN3](https://github.com/NVlabs/stylegan3)
ist in Punkto Bildqualität der vorherrschende generative Algorithmus.

### Generierung
Im Notebook 'stylegan2_faces_unconditional.ipynb' generieren wir zuerst zufällige Bilder.

![](https://miro.medium.com/max/1400/1*WR5OApYceVhZTNhO33csZw.png)

### Interpolation
Dann Interpolieren wir zwischen zwei Bildern. Beispielsweise vereint das Bild oben rechts Features der beiden linken Bilder.
Das Netz versucht gewissermaßen zu generieren, was als eine Art statistisches Mittel der Eigenschaften beider Bilder interpretiert werden könnte.

![](https://github.com/jwb95/HfG-KI-LAB---Tools/blob/main/StyleGAN2/media/interpolations/2_interp_ffhq.png?raw=true)

### Projektion
Anschließend unternehmen wir den Versuch Bilder in den Latent-Space von StyleGAN zu projizieren. Das bedeutet, StyleGAN soll probieren ein Bild
von uns selbstständig zu generieren - anschließend könnten wir dieses Bild etwa mit anderen Bildern interpolieren.
Dabei ist StyleGAN nicht unbedingt robust. Der Versuch ein Portrait in komplizierter Pose in Latent-Space von StyleGAN2 (trainiert mit Metfaces) zu projizieren
erwies sich als schwierig:

#### Original

![](https://github.com/jwb95/HfG-KI-LAB---Tools/blob/main/StyleGAN2/media/projections/originals/cot.jpg?raw=true)

#### Projektion in StyleGAN2-Metfaces

![](https://github.com/jwb95/HfG-KI-LAB---Tools/blob/main/StyleGAN2/media/projections/cot_proj.png?raw=true)

In [dieser Repo](https://github.com/woctezuma/stylegan2-projecting-images) wird gezeigt, wie unter Hinzunahme des Preprocessings, welches die StyleGAN-Autoren
für FFHQ benutzten, die Qualität von Projektionen gesteigert werden kann.

![](https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/gif/movie0001-opt.gif)

### Layer Blending

Im Notebook 'stylegan2_layerblend.ipynb' kann die Layer-Blending-Technik schnell ausprobiert werden.
Ein StyleGAN-Generator besteht aus verschiedenen Layern. Man kann es sich in etwa so vorstellen, dass die ersten Layer die gröbsten Formen generieren und
die darauf folgenden Layer konsekutiv Details hinzufügen. Mit Metfaces und FFHQ haben wir jeweils GANs, die Portraits generieren sollen, jedoch bestehen die Daten
von FFHQ aus Portrait-Photos und die Daten von Metfaces aus Photos von gemalten Portraits.
Es wäre nun denkbar die späteren Layers von Metfaces und die frühen von FFHQ zu nutzen, sodass wir ein Model erhalten, welches die Versalität von Form und Pose von
FFHQ und gleichzeitig die malerische Ästethik von Metfaces erhalten.

![](https://levindabhi.github.io/post/generating-different-styles/p3_huacd96a249b1a00c45f247a7befa1bed6_2779079_2000x2000_fit_lanczos_2.png)

Dieser[Blogpost](https://www.justinpinkney.com/stylegan-network-blending/) zeigt eine detaillierte Auseinandersetzung mit der Technik und liefert ein weiteres
[Notebook](https://github.com/justinpinkney/toonify/blob/master/StyleGAN-blending-example.ipynb
), mittels dessen zwischen FFHQ und einem auf Erdansichten trainierten StylenGAN geblendet werden kann.


### Wikiart

Die verbleibenden beiden Notebooks 'stylegan2_wikiart_unconditional.ipynb' und 'stylegan2_wikiart_conditional.ipynb' widmen sich der Synthese von Bildern
mit auf dem Wikiart-Datenset trainierten StyleGANs.
