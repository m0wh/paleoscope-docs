# Contribuer à la documentation

Cette documentation fonctionne avec [Docsify](https://docsify.js.org). Le contenu est rédgié en Markdown, un langage de balisage très simple à lire et à écrire qui permet de formatter les documents.

## Les bases du Markdown

### Titres

<!-- tabs:start -->

#### **Markdown**

```markdown
# Heading 1
## Heading 2
### Heading 3
```

#### **Resultat**

# Heading 1

## Heading 2

### Heading 3

<!-- tabs:end -->

### Gras et italique

<!-- tabs:start -->

#### **Markdown**

```markdown
**bold** __bold__
*italic* _italic_
```

#### **Resultat**

**bold** __bold__

*italic* _italic_

<!-- tabs:end -->

### Citation

<!-- tabs:start -->

#### **Markdown**

```
> Lorem Ipsum dolor
!> Attention
?> Info
```

#### **Resultat**

> Lorem Ipsum dolor

!> Attention

?> Info

<!-- tabs:end -->

### Liste ordonnée

<!-- tabs:start -->

#### **Markdown**

```markdown
1. Item
2. Item
3. Item
```

#### **Resultat**

1. Item
2. Item
3. Item

<!-- tabs:end -->

### Liste à puces

<!-- tabs:start -->

#### **Markdown**

```markdown
- Item
- Item
- Item
```

#### **Resultat**

- Item
- Item
- Item

<!-- tabs:end -->

### Liste de tâches

<!-- tabs:start -->

#### **Markdown**

```markdown
- [x] Item
- [ ] Item
- [ ] Item
```

#### **Resultat**

- [x] Item
- [ ] Item
- [ ] Item

<!-- tabs:end -->

### Code

<!-- tabs:start -->

#### **Markdown**

````markdown
`inline code`
````

````markdown
```javascript
console.log('code block')
```
````

#### **Resultat**

`inline code`

```javascript
console.log('code block')
```

<!-- tabs:end -->

### Séparation horizontale

<!-- tabs:start -->

#### **Markdown**

```markdown
---
```

#### **Resultat**

---

<!-- tabs:end -->

### Lien

<!-- tabs:start -->

#### **Markdown**

```markdown
[title](https://www.example.com)
```

#### **Resultat**

[title](https://www.example.com)

<!-- tabs:end -->

### Image

<!-- tabs:start -->

#### **Markdown**

```markdown
![alt text](image.jpg)
```

#### **Resultat**

![alt text](_media/image.jpg)

<!-- tabs:end -->

## Plugins

### Onglets (docsify-tabs)

<!-- tabs:start -->

#### **Markdown**

```
<!-- tabs:start -->

#### **English**

Hello!

#### **French**

Bonjour!

#### **Italian**

Ciao!

<!-- tabs:end -->
```

#### **Resultat**


<!-- tabs:start -->

#### **English**

Hello!

#### **French**

Bonjour!

#### **Italian**

Ciao!

<!-- tabs:end -->

<!-- tabs:end -->

### Schémas (docsify-kroki)

<!-- tabs:start -->

#### **Markdown**

````
```seqdiag
seqdiag {
  browser  -> webserver [label = "GET /seqdiag/svg/base64"];
  webserver  -> processor [label = "Convert text to image"];
  webserver <-- processor;
  browser <-- webserver;
}
```
````

#### **Resultat**

```seqdiag
seqdiag {
  browser  -> webserver [label = "GET /seqdiag/svg/base64"];
  webserver  -> processor [label = "Convert text to image"];
  webserver <-- processor;
  browser <-- webserver;
}
```

<!-- tabs:end -->

### GLTF (docsify-gltfexplorer)

<!-- tabs:start -->

#### **Markdown**

````
```gltf
```
````

#### **Resultat**

```gltf
```

<!-- tabs:end -->
