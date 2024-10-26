![Matplotlib](https://github.com/user-attachments/assets/cd86e598-812c-45c8-88fa-0dc7215f88a2)

> Development of Matplotlib for Python.

#

Matplotlib is a popular, comprehensive library for creating static, animated, and interactive visualizations in Python. It provides an extensive range of plotting functions, enabling users to produce high-quality graphs, charts, and plots like line graphs, bar charts, scatter plots, histograms, and 3D plots. Designed with flexibility in mind, Matplotlib allows for detailed customization of figures, including colors, line styles, labels, and axes, giving users control over every aspect of the visual presentation. It integrates well with other libraries such as NumPy and pandas, making it a powerful tool for data analysis and scientific computing. Matplotlib is widely used in various fields like finance, engineering, and data science for its ease of use and versatility.

#
### Layers
<details><summary>Expand</summary>
<br>

![Matplotlib Layers](https://github.com/sourceduty/Matplotlib_Layers/assets/123030236/952ecb81-0138-4cb5-971f-510927a3bb7e)

> Overlay multiple plots or graphical elements on a single figure using Matplotlib.

#

The layers function allows overlaying multiple plot types or graphical elements on a single figure, with control over the z-order (stacking order) of each layer, enabling custom layered visualizations.

#
### Function Signature

```
def layers(layers_data, axes=None, order=None, show=True, save_path=None, **kwargs):
    """
    Overlay multiple plots or graphical elements on a single figure.
    """
```

#
### Parameters

layers_data (list of dicts): A list of dictionaries, each representing a layer with:

type (str): The plot type ("line", "scatter", "bar", etc.).

data (dict): Plot data, typically containing x and y keys with corresponding lists.

kwargs (dict, optional): Additional arguments specific to the plot type (e.g., color, label).

axes (matplotlib.axes.Axes, optional): The plotting area to overlay the layers. Creates a new axes if None.

order (list of int, optional): The stacking order of the layers. Defaults to the order provided in layers_data if None.

show (bool, optional): Whether to display the plot (True by default).

save_path (str, optional): Path to save the figure. If None, the figure is not saved.

**kwargs: Additional global customization arguments for the plot (e.g., title, xlabel, ylabel).

#
### Returns

matplotlib.figure.Figure: The figure object containing the layered plot.

matplotlib.axes.Axes: The axes object containing the layered plot.

#
### Testing

To ensure the layers function works as intended, comprehensive testing should be performed. This includes unit tests to validate the functionality with various types of plots and parameters, as well as testing edge cases such as:

- Empty layers_data
- Invalid order indices
- Different plot customizations and styles

#
### Documentation

Detailed documentation should be provided to guide users on how to use the layers function. This documentation should include:

- Descriptions of each parameter and their expected inputs
- Multiple usage examples with different plot types and customizations
- Explanations of the return values
- Potential use cases and best practices

The layers function should be integrated into the Matplotlib library's official documentation, complete with visual aids and examples, to help users understand and utilize this powerful tool for creating layered plots.

#
### Example Code

```
import matplotlib.pyplot as plt

def layers(layers_data, axes=None, order=None, show=True, save_path=None, **kwargs):
    """
    Overlay multiple plots or graphical elements on a single figure.
    """
    # Create figure and axes if not provided
    if axes is None:
        fig, ax = plt.subplots()
        axes = ax  # Assign to axes for consistency
    else:
        fig = axes.figure

    # Determine layer stacking order
    if order is None:
        order = range(len(layers_data))

    # Overlay each specified layer
    for idx in order:
        layer = layers_data[idx]
        plot_type = layer.get("type")
        data = layer.get("data")
        plot_kwargs = layer.get("kwargs", {})
        plot_kwargs.update(kwargs)

        if plot_type == "line":
            axes.plot(data["x"], data["y"], **plot_kwargs)
        elif plot_type == "scatter":
            axes.scatter(data["x"], data["y"], **plot_kwargs)
        elif plot_type == "bar":
            axes.bar(data["x"], data["y"], **plot_kwargs)
        # Additional plot types can be added here as needed

    # Display plot if show=True
    if show:
        plt.show()

    # Save the figure if a path is specified
    if save_path:
        fig.savefig(save_path)

    return fig, axes

# Example usage
layers_data = [
    {"type": "line", "data": {"x": [1, 2, 3], "y": [4, 5, 6]}, "kwargs": {"color": "blue", "label": "Line Plot"}},
    {"type": "scatter", "data": {"x": [1, 2, 3], "y": [6, 5, 4]}, "kwargs": {"color": "red", "label": "Scatter Plot"}},
    {"type": "bar", "data": {"x": [1, 2, 3], "y": [5, 6, 7]}, "kwargs": {"color": "green", "label": "Bar Plot"}}
]

fig, axes = layers(layers_data, order=[2, 0, 1], show=False)

# Customizing plot
axes.set_title("Layered Plot Example")
axes.set_xlabel("X-Axis")
axes.set_ylabel("Y-Axis")
axes.legend()

plt.show()
```

<br>
</details>

### Layer Animation
<details><summary>Expand</summary>
<br>

The concept of layering and animating plots in Matplotlib enhances the visualization capabilities of the library by allowing users to overlay multiple graphical elements and animate them over time. This approach is particularly useful for creating complex visualizations where different types of data are represented simultaneously on the same axes. For instance, a user might want to combine line plots, scatter plots, and bar charts to provide a comprehensive view of data trends, distributions, and comparisons in a single figure. The layering concept ensures that these elements can be customized independently while maintaining a clear stacking order, giving users precise control over the visual hierarchy and aesthetic details. Additionally, this method integrates seamlessly with Matplotlib's native plotting functionality, making it accessible to users already familiar with the library while extending its capability in a modular and intuitive way.

Animating layered plots adds another dimension to data visualization, transforming static figures into dynamic, time-evolving representations. The layer_animation function, for instance, allows users to animate multiple layers of data, showing changes over time or across steps in a process. This is valuable for visualizing time-series data, simulations, or any scenario where observing the evolution of variables is critical. By updating each layer frame by frame, users can create informative and engaging animations, making it easier to communicate complex information effectively. The ability to customize frame intervals, repeat animations, and save them in various formats (e.g., GIFs or video files) further enhances the function’s versatility, allowing users to create and share dynamic visual content in presentations, reports, or interactive applications.

#
### layer_animation Function Overview

The layer_animation function animates the layers created by the layers function, allowing for dynamic visualization of changes over time. This can be useful for visualizing time-series data, evolving distributions, or any dataset where changes over time or steps are meaningful.

#
### Function Signature

def layer_animation(layers_data, frames, interval=200, repeat=True, axes=None, save_path=None, **kwargs):
    """
    Animate multiple plots or graphical elements over time on a single figure.
    """

#
### Parameters

layers_data (list of dicts): 
    A list of dictionaries, each representing a layer. Each dictionary includes:
    
    - type (str): The plot type ("line", "scatter", "bar", etc.).
    - data (list of dicts): A list where each element contains x and y keys with data for that frame.
    - kwargs (dict, optional): Additional arguments specific to the plot type (e.g., color, label).

frames (int or list): 
    The number of frames in the animation or a list of frame indices.

interval (int, optional): 
    Delay between frames in milliseconds. Default is 200.

repeat (bool, optional): 
    Whether to repeat the animation when it reaches the end. Default is True.

axes (matplotlib.axes.Axes, optional): 
    The plotting area for the animation. Creates a new axes if None.

save_path (str, optional): 
    Path to save the animation as a video or gif file. If None, the animation is not saved.

**kwargs: 
    Additional global customization arguments for the plot (e.g., title, xlabel, ylabel).

<br>
</details>

#
### Related Links

[Python Architect](https://chatgpt.com/g/g-ltK2f7Fkk-python-architect)
<br>
[High Python](https://github.com/sourceduty/High_Python)

***
Copyright (C) 2024, Sourceduty - All Rights Reserved.
