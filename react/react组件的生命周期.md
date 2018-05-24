#react组件的生命周期

- componentWillMout：在渲染前调用，在客户端也在服务端
- componentDidMount： 在第一次渲染后调用，之后组件已经生成了对应的DOM结构，可以通过this.getDOMnode()来访问。如果想和其他的框架一起使用，可以在这个方法中调用setTimeout, setInterval 或者发送ajax请求等来操作，防止异步操作阻塞UI
- componentWillReceiveProps：在组件接收到一个新的prop（更新后）时被调用。这个方法在初始化render时不会被调用。
- shouldComponentUpdate: 返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用，可以在确认不需要更新组建时使用。
- componentWillUpdate: 在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。
- componentDieUpdate: 在组件完成更新后立即调用。在初始化时不会被调用
- componentWillUnmount: 在组件从DOM中移除的时候立刻被调用。


`
var Hello = React.createClass({
    getInitialState: function(){
        return {
            opacity: 1.0
        }
    },

    componentDidMount: function() {
        this.timer = setInterval(function() {
            var opacity = this.state.opacity
            opacity -= .05
            if(opacity < 0.1) {
                opacity = 1.0
            }
            this.setState({
                opacity: opacity
            })
        }.bind(this), 100)
    },

    render: function () {
        retrune (
            <div style={{opacity: this.state.opacity}}>
                Hello, {this.props.name}
            </div>
        )
    }
})

ReactDOM.render(
    <Hello name="world" />
    document.body
)

`

eg:


`    
    var Button = React.createClass({

    getInitialState: function() {
        return {
        data:0
        };
    },
    setNewNumber: function() {
        this.setState({data: this.state.data + 1})
    },
    render: function () {
        return (
            <div>
                <button onClick = {this.setNewNumber}>INCREMENT</button>
                <Content myNumber = {this.state.data}></Content>
            </div>
        );
        }
    })
    var Content = React.createClass({

    componentWillMount:function() {
        console.log('Component WILL MOUNT!')
    },
    componentDidMount:function() {
        console.log('Component DID MOUNT!')
    },
    componentWillReceiveProps:function(newProps) {
            console.log('Component WILL RECEIVE PROPS!')
    },
    shouldComponentUpdate:function(newProps, newState) {
            return true;
    },
    componentWillUpdate:function(nextProps, nextState) {
            console.log('Component WILL UPDATE!');
    },
    componentDidUpdate:function(prevProps, prevState) {
            console.log('Component DID UPDATE!')
    },
    componentWillUnmount:function() {
            console.log('Component WILL UNMOUNT!')
    },
    
        render: function () {
        return (
            <div>
            <h3>{this.props.myNumber}</h3>
            </div>
        );
        }
    });
    ReactDOM.render(
    <div>
        <Button />
    </div>,
    document.getElementById('example')
    );

`