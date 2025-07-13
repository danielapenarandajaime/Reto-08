# Reto-08

## OrderItems Class

```Python
class OrderItems:
    
    def __init__(self, order: "Order"):
        self.order = order
        self.items = order.items
    
    def __iter__(self):
        return iter(self.items)
    
    def __len__(self):
        return len(self.items)
    
    def __getitem__(self, index):
        return self.items[index]
    
    def __contains__(self, item):
        return item in self.items
    
    def __repr__(self):
        return f"OrderItems({self.items})"
    
    def get_all_attributes(self):
        attributes_list = []
        for item in self.items:
            attributes = {
                'name': getattr(item, '_name', None),
                'price': getattr(item, '_price', None),
                'type': item.__class__.__name__
            }
            
            if isinstance(item, Beverages):
                attributes['alcohol'] = item.get_alcohol()
            elif isinstance(item, Starters):
                attributes['portion'] = item.get_portion()
            elif isinstance(item, MainCourse):
                attributes.update({
                    'protein': item.get_protein(),
                    'spicy': item.get_spicy(),
                    'vegetarian': item.get_vegetarian()
                })
            elif isinstance(item, Desserts):
                attributes.update({
                    'level_sugar': item.get_level_sugar(),
                    'gluten_free': item.get_gluten_free()
                })
            elif isinstance(item, Extras):
                attributes['with_sausage'] = item.get_with_sausage()
            elif isinstance(item, KidsMenu):
                attributes['healthy'] = item.get_haealthy()
            
            attributes_list.append(attributes)
        
        return attributes_list
```
## Output
```
All attributes:
{'name': 'Coke', 'price': 5.4, 'type': 'Beverages', 'alcohol': False}
{'name': 'Spaghetti Bolognese', 'price': 16.7, 'type': 'MainCourse', 'protein': 'Meat', 'spicy': False, 'vegetarian': False}
{'name': 'Cheesecake', 'price': 8.9, 'type': 'Desserts', 'level_sugar': 'Medium', 'gluten_free': False}
```
