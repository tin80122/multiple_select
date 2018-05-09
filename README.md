# multiple_select
It's a simple multiple select tool that can change the order by yourself.

## Getting Started

### Prerequisites

The plugins we used:

boostrap 3.3.7
vue 2.0

Notes: 
1.Plugins are all including in my folder of repository.
2.knowing framework of Vue 2.0 is better.

```
all source code of plugins are in assets folder.
```

### Installing

It's very easy to use this tool.

1.pull the project to your local
```
git clone my repository link
```

2.start to change your options of select
```
default_columns: [
                {"title":"item1","name":"item1_v"},
                {"title":"item2","name":"item2_v"},
                {"title":"item3","name":"item3_v"}
            ],
like_columns: []
```

3.Extra notes about import and output options of select
####import data of options
set ajax in ready function of vue
```
ready : function() {
        var self = this;
        this.$http.get('your route of source of import data').then((response_data) => {
            
                var new_columns = self.columns;	
                
                var default_columns = response_data['default'];
                var customized_columns = response_data['customized'];

                //Init Default
                for(var i=0 ;i< default_columns.length;i++){
                    self.default_columns.$set(i,default_columns[i]);
                }
                //Initi customized_column 
                for(var i=0;i< customized_columns.length ; i++){
                    self.like_columns.$set(i,{"title":customized_columns[i].title,"name":customized_columns[i].name});
                }
       })

```

####output data of options
add save button on html
add save function in function of methods
```
save: function(){          
  var columns_ary = [];
  for(var i=0;i<this.like_columns.length;i++){
      columns_ary.push(this.like_columns[i].name);
  }
  var output_data = {
      "like_columns" : columns_ary,
  };
  var self = this;
  this.$http.post('your route of handle saved data',output_data).then((response) => {
      if (response.body.status === 'ok'){
      //add notice message after saving
        self.error_msg = "Updated Successfully";
      };
  }else{
      self.error_msg = "Updated Failed"
  }
}
```

## live demo
<a href="https://tin80122.github.io/multiple_select/multiple_select.html" target="_blank">Go to see demo page</a>

## Authors

* **Sasa Tsai** - [哲學人的程式腦自學Note](https://sasacode.wordpress.com/)
