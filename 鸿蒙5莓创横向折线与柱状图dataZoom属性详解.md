### Hello and welcome back to our special session on HarmonyOS 5 Berry Creative chart components. In this episode, we'll explore the **dataZoom** property in the **McLineBarChart** combination chart component. The dataZoom component enables regional zooming, allowing users to focus on detailed data—especially useful for handling large datasets.  


### Detailed Explanation of `dataZoom` Properties  

#### 1. `show` Property  
**Function**: Toggles the visibility of the dataZoom scrollbar at the bottom of the chart.  
**Type**: Boolean  
**Default**: `false` (hidden)  

**Options**:  
- `true`: Show dataZoom component  
- `false`: Hide dataZoom component  

**Scenario**: Enable when there are many data points (e.g., >7) to facilitate viewing specific data ranges.  

**Code Example**:  
```typescript  
@State dataZoomOption: Options = new Options({  
  dataZoom: {  
    show: true  // Enable dataZoom  
  },  
  // Other configurations...  
})  
```  


#### 2. `start` Property  
**Function**: Sets the starting position of the scrollbar (index of the first visible data point).  
**Type**: Number  
**Default**: 0 (starts at the first data point)  
**Range**: Integer from 0 to (data length - 1)  

**Scenario**: Use to display a specific segment of data by default.  

**Code Example**:  
```typescript  
@State dataZoomOption: Options = new Options({  
  dataZoom: {  
    show: true,  
    start: 3  // Start at the 4th data point  
  },  
  // Other configurations...  
})  
```  


#### 3. `end` Property  
**Function**: Sets the ending position of the scrollbar (index of the last visible data point).  
**Type**: Number  
**Default**: 6 (ends at the 7th data point)  
**Range**: Integer from `start` to (data length - 1)  

**Scenario**: Control the default visible data range in combination with `start`.  

**Code Example**:  
```typescript  
@State dataZoomOption: Options = new Options({  
  dataZoom: {  
    show: true,  
    start: 2,  
    end: 5  // End at the 6th data point  
  },  
  // Other configurations...  
})  
```  


#### 4. `velocity` Property  
**Function**: Controls the scroll speed (higher values mean faster scrolling).  
**Type**: Number  
**Default**: 0 (default speed)  
**Range**: Positive numbers (recommended: 0–10)  

**Scenario**: Adjust the manual scrolling speed.  

**Code Example**:  
```typescript  
@State dataZoomOption: Options = new Options({  
  dataZoom: {  
    show: true,  
    velocity: 2  // Faster scrolling speed  
  },  
  // Other configurations...  
})  
```  


#### 5. `num` Property  
**Function**: Sets the difference between the maximum and minimum scroll values, limiting the zoom range.  
**Type**: Number  
**Default**: 0 (auto-calculated)  
**Range**: Positive numbers  

**Scenario**: Restrict the scrollable range (typically auto-calculated if not specified).  

**Code Example**:  
```typescript  
@State dataZoomOption: Options = new Options({  
  dataZoom: {  
    show: true,  
    num: 10  // Set scroll range difference  
  },  
  // Other configurations...  
})  
```  


### Complete Code Example  
Here's a full example demonstrating all `dataZoom` properties:  

```typescript  
import { McLineBarChart, Options } from '@mcui/mccharts'  

@Entry  
@Component  
struct Index {  
  @State dataZoomOption: Options = new Options({  
    title: {  
      show: true,  
      text: 'Complete dataZoom Example',  
      right: 20,  
      top: 22  
    },  
    xAxis: {  
      data: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']  
    },  
    yAxis: {  
      name: 'Sales (¥10,000)'  
    },  
    dataZoom: {  
      show: true,    // Enable dataZoom  
      start: 2,      // Start at the 3rd month  
      end: 8,        // End at the 9th month  
      velocity: 1.5, // Scroll speed  
      num: 6         // Scroll range difference  
    },  
    series: [  
      {  
        name: 'Sales',  
        data: [120, 132, 101, 134, 90, 230, 210, 182, 191, 234, 290, 330],  
        type: 'bar'  
      }  
    ]  
  })  

  build() {  
    Row() {  
      McLineBarChart({ options: this.dataZoomOption })  
    }  
    .height('50%')  
  }  
}  
```  


### Practical Use Cases  
The dataZoom component is invaluable in scenarios such as:  
1. **Long time-series data**: Viewing 365 days of data with ease.  
2. **Multi-data point comparison**: Focusing on specific categories in large datasets.  
3. **Mobile displays**: Allowing users to explore compressed data on small screens.  
4. **Data exploration**: Enhancing interactivity by enabling free-range zooming.  

**Example**: An e-commerce platform's annual sales report with mobile-friendly navigation:  
```typescript  
@State salesOption: Options = new Options({  
  // ...other configurations  
  dataZoom: {  
    show: true,  
    start: 0,  
    end: 3  // Default: Show Q1 data  
  }  
})  
```  
Users can scroll to view other quarters without page navigation.  


### Notes & Best Practices  
1. **Avoid dataZoom for small datasets** (<7 points) as full data is already visible.  
2. Ensure `end` > `start` for valid configurations.  
3. **Recalculate `start`/`end`** when dynamically updating data lengths.  
4. **Lower `velocity`** in performance-sensitive scenarios to optimize scrolling.  


### Conclusion  
That wraps up our guide to the `dataZoom` property! Master this powerful feature to provide users with intuitive data exploration capabilities. If you have questions, leave them in the comments. See you next time! 🚀
