pragma solidity ^0.4.13;

//класс доступа только для владельца
contract Ownable 
{
    // адрес владельца
    address owner;
    
    // запись адреса владельца
    function Ownable() 
    {
        owner = msg.sender;
    }
    
    // модификатор для запрета на запись (вызывать функцию может только владелец)
    modifier onlyOwner() 
    {
        require(msg.sender == owner);
        _;
    }
    
    function transferOwnership(address newOwner) onlyOwner 
    {
        owner = newOwner;
    }
}

contract BasisTokenCoin is Ownable
{
    
    // имя токкена
    string public constant name = "Basis Coint Token";
    // краткое имя валюты, символ
    string public constant symbol = "BCT";
    // знаки после запятой
    uint32 public constant decimals = 18;
    
    uint public totalSupply = 0;
    // массив с данными о покупателях адреса и токкены
    mapping (address => uint) balances;
    
    // запрос баланса токкена на кошельке
    function balanceOf(address _owner) constant returns (uint balance) 
    {
        return balances[_owner];
    }
    
    // передача токкена покупателю
    function transfer(address _to, uint _value) returns (bool success) 
    {
        // проверка на запрос токкенов больше, чем есть на кошельке / проверка на переполнение переменной
        if(balances[msg.sender] >= _value && balances[_to] + _value >= balances[_to])
        {
            // если проверка прошла успешно
            // берем запрошенное кол-во токкенов с кошелька
            balances[msg.sender] -= _value; 
            // прибавляем токкены к кошельку владельца
            balances[_to] += _value;
            // вызываем событие на отправку токкенов
            Transfer(msg.sender, _to, _value);
            return true;
        }
        return false;
    }
    
    // передача токкена от одного лица к другому
    function transferFrom(address _from, address _to, uint _value) returns (bool success) 
    {
        // проверка на запрос токкенов больше, чем есть на кошельке / проверка на переполнение переменной
        if(balances[_from] >= _value && balances[_to] + _value >= balances[_to])
        {
            // если проверка прошла успешно
            // берем запрошенное кол-во токкенов с кошелька
            balances[_from] -= _value; 
            // прибавляем токкены к кошельку владельца
            balances[_to] += _value;
            // вызываем событие на отправку токкенов
            Transfer(_from, _to, _value);
            return true;
        }
        return false;
    }
    
    // проивзодим монетки, её может вызвать только хозяин
    function mint(address _to, uint _value) onlyOwner 
    {
      assert(totalSupply + _value >= totalSupply && balances[_to] + _value >= balances[_to]);
      balances[_to] += _value;
      totalSupply += _value;
    }
    
    //
    function approve(address _spender, uint _value) returns (bool success) 
    {
        return false;
    }
    
    function allowance(address _owner, address _spender) constant returns (uint remaining) 
    {
        return 0;
    }
    
    // событие передачи токена
    event Transfer(address indexed _from, address indexed _to, uint _value);
    
    event Approval(address indexed _owner, address indexed _spender, uint _value);
    
}
