ajax 加载ztree

	$(document).ready(function(){	
			$(function(){
				//tree node json数据加载	
	
				 $.post('TreeNodeServlet',function(data){
						if(data !=null){
							var dataObj =eval("("+ data+")");
			
							//alert(dataObj.carInfoNodes);	
							carOntologyNodes=dataObj.carOntologyNodes;
							carInfoNodes= dataObj.carInfoNodes;
							//alert("carInfoNodes-----"+carInfoNodes);
							//注意znode前要加操作eval
							$.fn.zTree.init($("#treeDemo"), setting, eval(carOntologyNodes));
				
							$.fn.zTree.init($("#treeDemo2"), setting2, eval(carInfoNodes));	
						}
					});	

			/**	第二种方法
				$.ajax({
					type:"post",
					url:"TreeNodeServlet",
					success:function(data){
						if(data !=null){
							var dataObj =eval("("+ data+")");
			
							//alert(dataObj.carInfoNodes);	
							carOntologyNodes=dataObj.carOntologyNodes;
							carInfoNodes= dataObj.carInfoNodes;
							$.fn.zTree.init($("#treeDemo"), setting, eval(carOntologyNodes));
							$.fn.zTree.init($("#treeDemo2"), setting2, eval(carInfoNodes));	
						}
					}
				});
				**/
			});	
		});