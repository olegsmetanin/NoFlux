# NoFlux
NoFlux Architecture

```javascript
Repository extends EventEmitter, StateSetter {
  noun() {
    if (!this.state.noun) {
      httprequest.exec().then(noun => this.setState({noun: noun}));
    }
    return this.state.noun;
  }
}

Action {
  async action() {
    var actionValue = await this.actionX();
    return await httprequest.exec();
  }
}

Cache extends LRU {

}

class ReactComponent extends React.Component {

  constructor(props, context) {
    super(props, context);
    this.state = {
      data: context.cache.get(),
      me: context.userRepository.me()
    }
  }

  componentDidMount() {
    this.userRepository.addEventListener('change', this.getFromUserRepository);
  }

  componentWillMount() {
    this.userRepository.removeEventListener('change', this.getFromUserRepository);
  }

  getFromUserRepository(user) {
  }

  onSend() {
    this.someActions.someAction().then(
      data => this.setState(),
      err => this.setState()
    )
  }

}
```


![React-Repository](http://g.gravizo.com/g?
%40startuml%0A%0AReact%20-%3E%20Repository%3A%20noun%0Aactivate%20React%0A%0ARepository%20-%3E%20WS%3A%20noun%2Fget%0Aactivate%20Repository%0A%0AWS%20--%3E%20Repository%3A%20%0Adeactivate%20Repository%0A%0ARepository%20--%3E%20React%3A%20%0Adeactivate%20Repository%0A%0A%40enduml%0A%20%20%20%20%20%20%20%20%20%20%20%20)

![React-Action](http://g.gravizo.com/g?
%40startuml%0A%0AReact%20-%3E%20Action%3A%20verb%0Aactivate%20React%0A%0AAction%20-%3E%20WS%3A%20noun%2Fverb%0Aactivate%20Action%0A%0AWS%20--%3E%20Action%3A%20%0Adeactivate%20Action%0A%0AAction%20--%3E%20React%3A%20%0Adeactivate%20React%0A%0A%40enduml%0A%20%20%20%20%20%20%20%20%20%20%20%20)

![React-Action](http://g.gravizo.com/g?
%40startuml%0A%0AReact%20-%3E%20Cache%0Aactivate%20React%0A%0ACache%20--%3E%20React%0Adeactivate%20React%0A%0A%40enduml%0A%20%20%20%20%20%20%20%20%20%20%20%20)


