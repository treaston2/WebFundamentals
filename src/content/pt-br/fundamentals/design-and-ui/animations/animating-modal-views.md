project_path: /web/_project.yaml
book_path: /web/fundamentals/_book.yaml
description: Aprenda como animar visualizações modais em seus aplicativos.


{# wf_updated_on: 2014-10-20 #}
{# wf_published_on: 2014-08-08 #}

# Animating Modal Views {: .page-title }

{% include "web/_shared/contributors/paullewis.html" %}


As visualizações modais são para mensagens importantes e, por isso, você tem bons motivos para bloquear a interface do usuário. Deve-se tomar cuidado ao usá-las pois elas incomodam podem e facilmente arruinar a experiência do usuário se utilizadas em excesso. Mas, em algumas situações, são a alternativa correta e um pouco de animação dará vida às visualizações.

### TL;DR {: .hide-from-toc }
- As visualizações modais devem ser usadas com moderação; os usuários ficarão frustrados se você interromper a experiência deles desnecessariamente.
- Adicionar escala à animação proporciona um bom efeito de ‘queda’.
- Certifique-se de remover a visualização modal rapidamente quando o usuário descartá-la, mas ela deve ser exibida na tela um pouco mais lentamente para não surpreender o usuário.


<img src="images/dont-press.gif" alt="Animando uma visualização modal." />

<a href="https://googlesamples.github.io/web-fundamentals/fundamentals/design-and-ui/animations/modal-view-animation.html">Veja a amostra.</a>

A sobreposição modal deve ser alinhada com a porta de visualização, portanto, precisa de seu `position` definido para `fixed`:


    .modal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
    
      pointer-events: none;
      opacity: 0;
    
      will-change: transform, opacity;
    }
    

Tem um `opacity` inicial de 0, portanto, está oculto na visualização. Mas também precisará de `pointer-events` definido para `none` para que o clique e o toque sejam transmitidos. Sem isso, todas as interações serão bloqueadas e a página ficará sem resposta. Por fim, como seu `opacity` e `transform` serão animados, eles precisam ser marcados como mudando com `will-change` (veja também [Usando a propriedade will-change](/web/fundamentals/design-and-ui/animations/animations-and-performance#using-the-will-change-property)).

Quando a visualização estiver visível, as interações precisarão ser aceitas e um `opacity` de 1 será necessário:


    .modal.visible {
      pointer-events: auto;
      opacity: 1;
    }
    

Agora, sempre que a visualização modal for necessária, você pode usar o JavaScript para alternar a classe “visible”:


    modal.classList.add('visible');
    

Neste ponto, a visualização modal aparecerá sem qualquer animação. Portanto, agora ela poderá ser adicionada
(veja também [Easing personalizado](/web/fundamentals/design-and-ui/animations/custom-easing)):


    .modal {
      -webkit-transform: scale(1.15);
      transform: scale(1.15);
    
      -webkit-transition:
        -webkit-transform 0.1s cubic-bezier(0.465, 0.183, 0.153, 0.946),
        opacity 0.1s cubic-bezier(0.465, 0.183, 0.153, 0.946);
    
      transition:
        transform 0.1s cubic-bezier(0.465, 0.183, 0.153, 0.946),
        opacity 0.1s cubic-bezier(0.465, 0.183, 0.153, 0.946);
    
    }
    

Adicionar `scale` à transformação faz com que a visualização pareça cair na tela suavemente, o que é um bom efeito. A transição padrão é aplicada às propriedades transform e opacity com uma curva personalizada e uma duração de 0,1 segundo.

A duração é muito curta, mas é ideal para quando o usuário descartar a visualização e desejar voltar para o seu aplicativo. O ponto negativo é que provavelmente seja muito agressivo para quando a visualização modal for exibida. Para corrigir isso, você deve substituir os valores de transição para a classe `visible`:


    .modal.visible {
    
      -webkit-transform: scale(1);
      transform: scale(1);
    
      -webkit-transition:
        -webkit-transform 0.3s cubic-bezier(0.465, 0.183, 0.153, 0.946),
        opacity 0.3s cubic-bezier(0.465, 0.183, 0.153, 0.946);
    
      transition:
        transform 0.3s cubic-bezier(0.465, 0.183, 0.153, 0.946),
        opacity 0.3s cubic-bezier(0.465, 0.183, 0.153, 0.946);
    
    }
    

Agora, a visualização modal leva 0,3 segundo para aparecer na tela, que é um pouco menos agressivo. Mas é descartada rapidamente, e o que agradará o usuário.



