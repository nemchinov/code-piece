1. Использовать PropTypes
    ```javascript
    import PropTypes from 'prop-types';

    class Greeting extends React.Component { }

    Greeting.propTypes = {
        name: PropTypes.string
    };
    // optionalElement: PropTypes.element // A React element
    // optionalMessage: PropTypes.instanceOf(Message)
    // optionalEnum: PropTypes.oneOf(['News', 'Photos'])
    // optionalArrayOf: PropTypes.arrayOf(PropTypes.number)
    // optionalObjectWithShape: PropTypes.shape({
    //   color: PropTypes.string,
    //   fontSize: PropTypes.number
    // })
    // requiredFunc: PropTypes.func.isRequired //  Обязательный параметр
    // requiredAny: PropTypes.any.isRequired

    Greeting.defaultProps = {
        name: 'Stranger'
    };
    ```
