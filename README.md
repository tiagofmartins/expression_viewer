# Expression Viewer

_Introductory text and screenshot soon._

## Expression editing

There are two methods for modifying the input expression:

1. **Code variable:** You can insert the expression string in the variable `expression` (located at the beginning of the code) before running the visualiser.
2. **Text file:** You can store the expression string in the file `expression.txt` which is continuously watched by the visualiser for modifications. By default this file is located inside the folder `expression_viewer/data/`, but you can easily change this my modifying the variable `expressionFile` (located at the beginning of the code). This method is useful for live expression editing or to visualise expression being generated programmatically.

Please note that the second method overrides the first. Thus, if there is an expression saved in the file, this will be the one that will be visualised (ignoring the expression specified in the code).

## Integration with Genetic Programming engine

The integration of this tool with a GP engine allows rendering the output (image) of each tree node. Specifically, the visualiser asks the GP engine to generate images for a set of expressions, including the input expression and all of its subexpressions. Once these images are generated and saved in a particular folder, the visualiser loads and displays them in the tree. Whenever the expression changes, the visualiser asks the GP engine for new images.

This integration requires the GP engine to:

<pre>
Repeat:
    If file <b>gp_engine_order.txt</b> exists:
        Read value <b>image_size</b> from this file
        Read path <b>gp_engine_images</b> from this file
        Read path <b>gp_engine_feedback</b> from this file
        Read list of expressions (and each corresponding id) from this file
        If folder <b>gp_engine_images</b> exists:
            Remove contents of this folder
        Else:
            Create this folder
        Create empty list <b>errors</b>
        For each expression:
            Generate image with size <b>image_size</b>
            If image was created successfully:
                Save image in folder <b>gp_engine_images</b> with the filename <b><i>id</i>.png</b>
            Else:
                Add to list <b>errors</b> one text line describing the error that occured        
            Create folder <b>gp_engine_images</b>
        Create file <b>gp_engine_feedback.txt</b> containing the list <b>errors</b>
        Delete file <b>gp_engine_order.txt</b>
</pre>

The file `gp_engine_order.txt` is located by default inside the folder `expression_viewer/data/`. However, this can be changed in the variable `fileWithGPEngineOrder` in the visualiser code.

## Interaction

- Press key `e` to see or edit the input expression using the default external editor
