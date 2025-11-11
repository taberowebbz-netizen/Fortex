
# 🎨 Guia de Criação de Ícones - Fortex

## Ícones Necessários

### 1. icon-192.png (192x192px)
- **Formato**: PNG
- **Fundo**: Transparente ou azul (#2B7FFF)
- **Design**: Logo Fortex (moeda dourada/azul)
- **Uso**: Ícone principal do app

### 2. icon-512.png (512x512px)
- **Formato**: PNG
- **Fundo**: Transparente ou azul (#2B7FFF)
- **Design**: Logo Fortex em alta resolução
- **Uso**: Splash screen e instalação

### 3. favicon.ico (32x32px)
- **Formato**: ICO
- **Design**: Versão simplificada do logo
- **Uso**: Ícone do navegador

### 4. screenshot-1.png (540x720px)
- **Formato**: PNG
- **Conteúdo**: Captura da tela principal de mineração
- **Uso**: World App Store listing

## Ferramentas Recomendadas

### Online (Gratuitas)
1. **Canva** - https://canva.com
   - Template: "App Icon"
   - Dimensões: 192x192 e 512x512
   - Exportar como PNG

2. **Figma** - https://figma.com
   - Criar frame 512x512
   - Adicionar logo/design
   - Exportar em múltiplas resoluções

3. **RealFaviconGenerator** - https://realfavicongenerator.net
   - Upload do icon-512.png
   - Gera todos os formatos automaticamente

### Desktop
- **GIMP** (gratuito) - https://gimp.org
- **Photoshop** (pago)
- **Affinity Designer** (pago)

## Design Sugerido

### Conceito Visual
```
┌─────────────────┐
│                 │
│   🪙 FORTEX    │  ← Moeda dourada/azul
│                 │
│   Gradiente     │  ← Fundo azul (#2B7FFF)
│   Azul/Roxo     │     para roxo (#6366f1)
│                 │
└─────────────────┘
```

### Cores do Fortex
- **Primário**: #2B7FFF (Azul)
- **Secundário**: #6366f1 (Roxo/Indigo)
- **Acento**: #F59E0B (Dourado)
- **Fundo**: #0A0A0A (Preto)

### Elementos Visuais
- Moeda/token no centro
- Efeito de brilho/glow
- Bordas arredondadas (iOS style)
- Sombra sutil

## Passos Rápidos (Canva)

1. Acesse https://canva.com
2. Crie design → "App Icon" (1024x1024)
3. Adicione círculo azul (#2B7FFF)
4. Adicione texto "FTX" ou símbolo de moeda
5. Aplique gradiente azul → roxo
6. Baixe como PNG
7. Redimensione para 192x192 e 512x512

## Converter para Favicon

```bash
# Usando ImageMagick (Linux/Mac)
convert icon-192.png -resize 32x32 favicon.ico

# Ou use: https://favicon.io/favicon-converter/
```

## Captura de Screenshot

1. Abra o app em produção
2. Use DevTools (F12) → Device Toolbar
3. Selecione "iPhone 12 Pro" (390x844)
4. Navegue para tela principal
5. Capture screenshot (Ctrl+Shift+P → "Capture screenshot")
6. Redimensione para 540x720

## Checklist Final

- [ ] icon-192.png criado e otimizado
- [ ] icon-512.png criado e otimizado
- [ ] favicon.ico criado
- [ ] screenshot-1.png capturado
- [ ] Todos os arquivos na pasta `public/`
- [ ] Testado em dispositivo real
- [ ] Validado no Lighthouse (PWA score)

## Validação

### Testar Ícones
1. Coloque os arquivos em `public/`
2. Execute `npm run build`
3. Abra DevTools → Application → Manifest
4. Verifique se os ícones aparecem corretamente

### Lighthouse Audit
```bash
# Chrome DevTools
1. F12 → Lighthouse
2. Selecione "Progressive Web App"
3. Generate report
4. Score deve ser > 90
```

## Recursos Adicionais

- **Imagem Base**: https://images.unsplash.com/photo-1621416894569-0f39ed31d247
- **Paleta de Cores**: https://coolors.co/2b7fff-6366f1-f59e0b
- **Icon Generator**: https://www.pwabuilder.com/imageGenerator

---

**Após criar os ícones, delete o arquivo `public/icon-placeholder.txt`**
