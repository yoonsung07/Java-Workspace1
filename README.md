# Java-Workspace1

package edu.ou.cs.hci.assignment.prototypea.pane; // Added package

import edu.ou.cs.hci.assignment.prototypea.Controller;
import javafx.beans.value.ObservableValue;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Insets;
import javafx.geometry.Orientation;
import javafx.geometry.Pos;
import javafx.scene.control.Button;
import javafx.scene.control.CheckBox;
import javafx.scene.control.Label;
import javafx.scene.control.Slider;
import javafx.scene.control.Spinner;
import javafx.scene.control.TextArea;
import javafx.scene.control.TextField;
import javafx.scene.image.ImageView;
import javafx.scene.layout.Border;
import javafx.scene.layout.BorderPane;
import javafx.scene.layout.BorderStroke;
import javafx.scene.layout.BorderStrokeStyle;
import javafx.scene.layout.BorderWidths;
import javafx.scene.layout.CornerRadii;
import javafx.scene.layout.FlowPane;
import javafx.scene.layout.HBox;
import javafx.scene.layout.Pane;
import javafx.scene.layout.VBox;
import javafx.scene.paint.Color;
import javafx.scene.text.Font;
import javafx.scene.text.FontPosture;
import javafx.scene.text.Text;

//******************************************************************************

/**
 * The <CODE>EditorPane</CODE> class.
 *
 * @author  Chris Weaver
 * @version %I%, %G%
 */
public final class EditorPane extends AbstractPane
{
	//**********************************************************************
	// Private Class Members
	//**********************************************************************

	private static final String	NAME = "Editor";
	private static final String	HINT = "Movie Metadata Editor";

	//**********************************************************************
	// Private Class Members (Effects)
	//**********************************************************************

	private static final Font FONT_LARGE =
		Font.font("Serif", FontPosture.ITALIC, 24.0);

	private static final Font FONT_SMALL =
		Font.font("Serif", FontPosture.ITALIC, 18.0);

	//**********************************************************************
	// Private Members
	//**********************************************************************

	// Layout (a few widgets)
	private Slider slider;

	private Spinner<Integer> spinner;

	private TextField textField;
	private TextField textRating;
	private TextField textYear;
	private TextField textAge;
	
	private TextArea textArea;
	private TextArea textSummary;
	
	private CheckBox checkBox1;
	private CheckBox checkBox2;
	private CheckBox checkBox3;
	private CheckBox checkBox4;
	private CheckBox checkBox5;
	private CheckBox checkBox6;
	
	private CheckBox checkBox7;
	private CheckBox checkBox8;
	private CheckBox checkBox9;
	private CheckBox checkBox10;
	private CheckBox checkBox11;
	private CheckBox checkBox12;
	
	private Button awakenButton;
	
	// Support
	private boolean ignoreCaretEvents;
	
	// Handlers
	private final ActionHandler	actionHandler;

	//**********************************************************************
	// Constructors and Finalize(r)
	//**********************************************************************

	public EditorPane(Controller controller) 
	{
		super(controller, NAME, HINT);
		actionHandler = new ActionHandler();

		//setBase(buildPane()); // <----------------------------------------------------- "Set Base Here!!"
		setBase(mainPane());
	}

	//**********************************************************************
	// Public Methods (Controller)
	//**********************************************************************

	// The controller calls this method when it adds a view.
	// Set up the nodes in the view with data accessed through the controller.
	public void	initialize()
	{
		// Widget Gallery, Slider
		slider.setValue((Double)controller.get("myDouble"));

		// Widget Gallery, Spinner
		spinner.getValueFactory().setValue((Integer)controller.get("myInt"));

		// Widget Gallery, Text Field
		textField.setText((String)controller.get("myString"));
		textRating.setText((String)controller.get("myRating"));
		textYear.setText((String)controller.get("myYear"));
		textAge.setText((String)controller.get("myAge"));
		
		// Widget Gallery, Text Area
		textArea.setText((String)controller.get("comment"));
		textSummary.setText((String)controller.get("summary"));
		
		// Widget Gallery, Check Box
		checkBox1.setSelected((Boolean)controller.get("Action"));
		checkBox2.setSelected((Boolean)controller.get("Adventure"));
		checkBox3.setSelected((Boolean)controller.get("Comedy"));
		checkBox4.setSelected((Boolean)controller.get("Drama"));
		checkBox5.setSelected((Boolean)controller.get("Fantasy"));
		checkBox6.setSelected((Boolean)controller.get("War"));
		
		checkBox7.setSelected((Boolean)controller.get("Is Animated:"));
		checkBox8.setSelected((Boolean)controller.get("Is Color:"));
		checkBox9.setSelected((Boolean)controller.get("Award Picture:"));
		checkBox10.setSelected((Boolean)controller.get("Award Directing:"));
		checkBox11.setSelected((Boolean)controller.get("Award Cinematography:"));
		checkBox12.setSelected((Boolean)controller.get("Award Acting:"));
		
	}

	// The controller calls this method when it removes a view.
	// Unregister event and property listeners for the nodes in the view.
	public void	terminate()
	{
		// Widget Gallery, Slider
		slider.valueProperty().removeListener(this::changeDecimal);

		// Widget Gallery, Spinner
		spinner.valueProperty().removeListener(this::changeInteger);		
		// Widget Gallery, Text Field
		textField.setOnAction(null);
		textRating.setOnAction(null);
		textYear.setOnAction(null);
		textAge.setOnAction(null);
		// Widget Gallery, RadioButtons
		//radioButton1.setOnAction(null);
		//radioButton2.setOnAction(null);
		
		// Widget Gallery, Text Area
		textArea.textProperty().removeListener(this::changeComment);
		textSummary.textProperty().removeListener(this::changeComment);
				
		// Widget Gallery, Check Box
		checkBox1.setOnAction(null);
		checkBox2.setOnAction(null);
		checkBox3.setOnAction(null);
		checkBox4.setOnAction(null);
		checkBox5.setOnAction(null);
		checkBox6.setOnAction(null);
		
		checkBox7.setOnAction(null);
		checkBox8.setOnAction(null);
		checkBox9.setOnAction(null);
		checkBox10.setOnAction(null);
		checkBox11.setOnAction(null);
		checkBox12.setOnAction(null);
		
		// Widget Gallery, Buttons
		awakenButton.setOnAction(null);
	}

	// The controller calls this method whenever something changes in the model.
	// Update the nodes in the view to reflect the change.
	public void	update(String key, Object value)
	{
		//System.out.println("update " + key + " to " + value);
		if ("myDouble".equals(key))
		{
			slider.setValue((Double)value);
		}
		else if ("myInt".equals(key))
		{
			spinner.getValueFactory().setValue((Integer)value);
		}
		else if ("myString".equals(key))
		{
			textField.setText((String)value);
		}
		else if ("myRating".equals(key))
		{
			textRating.setText((String)value);
		}
		else if ("myYear".equals(key)) 
		{
			textYear.setText((String)value);
		}
		else if ("myAge".equals(key))
		{
			textAge.setText((String)value);
		}
		else if ("comment".equals(key))
		{
			ignoreCaretEvents = true;
			textArea.setText((String)value);
			ignoreCaretEvents = false;
		}
		else if ("summary".equals(key))
		{
			ignoreCaretEvents = true;
			textSummary.setText((String)value);
			ignoreCaretEvents = false;
		}
		else if ("Action".equals(key) || "Adventure".equals(key) || "Comedy".equals(key) ||
				 "Drama".equals(key) || "Fantasy".equals(key) || "War".equals(key))
		{
			if ("Action".equals(key)) 
				checkBox1.setSelected((Boolean)value);
			else if ("Adventure".equals(key))
				checkBox2.setSelected((Boolean)value);
			else if ("Comedy".equals(key))
				checkBox3.setSelected((Boolean)value);
			else if ("Drama".equals(key))
				checkBox4.setSelected((Boolean)value);
			else if ("Fantasy".equals(key))
				checkBox5.setSelected((Boolean)value);
			else if ("War".equals(key))
				checkBox6.setSelected((Boolean)value);
		}
		else if ("Is Animated:".equals(key) || "Is Color:".equals(key) || "Award Picture:".equals(key) ||
				 "Award Directing:".equals(key) || "Award Cinematography:".equals(key) || 
				 "Award Acting:".equals(key))
		{
			if ("Is Animated:".equals(key)) 
				checkBox7.setSelected((Boolean)value);
			else if ("Is Color:".equals(key))
				checkBox8.setSelected((Boolean)value);
			else if ("Award Picture:".equals(key))
				checkBox9.setSelected((Boolean)value);
			else if ("Award Directing:".equals(key))
				checkBox10.setSelected((Boolean)value);
			else if ("Award Cinematography:".equals(key))
				checkBox11.setSelected((Boolean)value);
			else if ("Award Acting:".equals(key))
				checkBox12.setSelected((Boolean)value);
		}
	}

	//**********************************************************************
	// Private Methods (Layout)
	//**********************************************************************
	/*
	private Pane buildPane()
	{
		// Layout the widgets in a vertical flow with small gaps between them.
		FlowPane pane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		pane.setAlignment(Pos.TOP_LEFT);

		pane.getChildren().add(createSlider());
		pane.getChildren().add(createSpinner());
		pane.getChildren().add(createTextField());

		return pane;
	}*/
	
	/*
	 * [Level 0] Main Layout Panel: Which holds the entire window of this program.
	 */
	private Pane mainPane() 
	{
		FlowPane pane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		pane.setAlignment(Pos.TOP_LEFT);
		
		// Adding the different "sub panes" into the FlowPane <pane>. 
		pane.getChildren().add(topTitlePane());
		pane.getChildren().add(topTitleBorderPane());
		pane.getChildren().add(bottomPane());
		
		return pane;
	}
	
	/*
	 * [Level 1] Top Panel: Which is placed the top section of the "Main Layout." Also the title of the window. 
	 */
	private Pane topTitlePane()
	{
		Text text = new Text("      JUMANJI: THE NEXT LEVEL REVIEWS & TALK");
		
		BorderPane.setAlignment(text, Pos.TOP_LEFT);
		
		BorderPane borderPane = new BorderPane();
		borderPane.setLeft(text);
		borderPane.setTranslateY(10); // Translate on the y-axis.
		
		return borderPane;
	}
	
	/*
	 * [Level 1] Underline Top Panel: Created an underline of the title. 
	 */
	private Pane topTitleBorderPane()
	{
		FlowPane pane = new FlowPane(30, 30);
		pane.setBorder(new Border(new BorderStroke(Color.BLACK, BorderStrokeStyle.SOLID, 
												CornerRadii.EMPTY, BorderWidths.DEFAULT)));
		pane.setTranslateX(5); // Translate on the x-axis.
		
		return pane;
	}
	
	/*
	 * [Level 1] Bottom Panel: Which will hold the information of many widgets and text. 
	 */
	private Pane bottomPane() 
	{
		FlowPane bpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		bpane.setAlignment(Pos.BOTTOM_LEFT);
		
		// Adding the leftPane & rightPane into the bottomPane.
		bpane.getChildren().add(leftPane());
		bpane.getChildren().add(rightPane());
		bpane.getChildren().add(middlerightPane());
		
		return bpane;
	}
	
	/*
	 * [Level 2] Left Panel: Which holds the left side of the "Bottom Panel." 
	 *                       This would have the image/border/radioButton. 
	 */
	private Pane leftPane() 
	{
		FlowPane lpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		lpane.setAlignment(Pos.BOTTOM_LEFT);

		lpane.getChildren().add(leftTopPane());
		lpane.getChildren().add(translateQuestionBox());
		lpane.getChildren().add(createdButtons());
			
		return lpane;
	}
	
	/*
	 * [Level 3] Top Area of Left Panel: Which will be the section that hold the Image of the movie.
	 */
	private Pane leftTopPane()
	{
		FlowPane ltpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		ltpane.setAlignment(Pos.TOP_LEFT);
		
		ltpane.getChildren().add(imagePane());
		
		return ltpane;
	}
	
	/*
	 * [Level 3] Button
	 */
	private Pane createdButtons()
	{
		FlowPane pane = new FlowPane(8.0, 8.0);
		pane.setAlignment(Pos.CENTER_LEFT);
		
		awakenButton = new Button("Import");
		awakenButton.setOnAction(actionHandler);
		
		pane.getChildren().add(awakenButton);
		
		pane.setTranslateX(-80);
		pane.setTranslateY(2);
		
		return pane;
	}
	
	/*
	 * [Level 4] Image View: This would hold the image and placed on the top left of
	 *                       the "Left Panel."
	 */
	private Pane imagePane() 
	{
		/*FileInputStream input;
		
		try {
			input = new FileInputStream("bin/main/edu/ou/cs/hci/resources/example/fx/icon/Jumanji.png");
		} catch (FileNotFoundException e) {
			e.printStackTrace();
			return null;
		}*/
		
		//Image image = new Image(/);
		//ImageView imageView = new ImageView(image);
		
		ImageView imageView = createFXIcon("Jumanji.png", 240, 360);
		
		BorderPane.setAlignment(imageView, Pos.TOP_LEFT);
		BorderPane borderPane = new BorderPane();
		borderPane.setLeft(imageView);
		borderPane.setTranslateX(80);
		borderPane.setTranslateY(0);
		
		return borderPane;
	}
	
	private Pane translateQuestionBox()
	{
		FlowPane box = new FlowPane(Orientation.HORIZONTAL, 8.0, 8.0);
		box.setAlignment(Pos.BOTTOM_LEFT);
		
		box.getChildren().add(questionBox());
		box.setTranslateY(200);
		box.setTranslateX(-225);
		
		return box;
	}
	
	private Pane questionBox()
	{
		checkBox7 = new CheckBox("Is Animated:");
		checkBox8 = new CheckBox("Is Color:");
		checkBox9 = new CheckBox("Award Picture:");
		checkBox10 = new CheckBox("Award Directing:");
		checkBox11 = new CheckBox("Award Cinematography:");
		checkBox12 = new CheckBox("Award Acting:");
		
		checkBox7.setOnAction(actionHandler);
		checkBox8.setOnAction(actionHandler);
		checkBox9.setOnAction(actionHandler);
		checkBox10.setOnAction(actionHandler);
		checkBox11.setOnAction(actionHandler);
		checkBox12.setOnAction(actionHandler);
		
		checkBox7.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		checkBox8.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		checkBox9.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		checkBox10.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		checkBox11.setPadding(new Insets(8.0, 4.0, 8.0, 4.0));
		checkBox12.setPadding(new Insets(8.0, 4.0, 8.0, 4.0));
		
		FlowPane box = new FlowPane(Orientation.HORIZONTAL, 8.0, 8.0);
		//box.setAlignment(Pos.BOTTOM_CENTER);
		
		box.getChildren().add(checkBox7);
		box.getChildren().add(checkBox8);
		box.getChildren().add(checkBox9);
		box.getChildren().add(checkBox10);
		box.getChildren().add(checkBox11);
		box.getChildren().add(checkBox12);
		
		return createTitledPane(box, "Is it: ");
	}

 /*
	private Pane radioButtonPane1()
	{		
		ToggleGroup tg = new ToggleGroup();
		
		Label topic = new Label(" Is Animated:	                 ");
		
		radioButton1 = new RadioButton("True");
		radioButton2 = new RadioButton("False");
		
		radioButton1.setOnAction(actionHandler);
		radioButton2.setOnAction(actionHandler);
		
		radioButton1.setToggleGroup(tg);
		radioButton2.setToggleGroup(tg);
		
		radioButton1.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		radioButton2.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		
		HBox box = new HBox();
		
		box.getChildren().addAll(topic, radioButton1, radioButton2);
		box.setTranslateX(-170);
		box.setTranslateY(90);
		
		return box;
	}
	
	private Pane radioButtonPane2()
	{
		ToggleGroup tg = new ToggleGroup();
		
		Label topic = new Label(" Is Color:	                         ");
		
		radioButton1 = new RadioButton("True");
		radioButton2 = new RadioButton("False");
		
		radioButton1.setOnAction(actionHandler);
		radioButton2.setOnAction(actionHandler);
		
		radioButton1.setToggleGroup(tg);
		radioButton2.setToggleGroup(tg);
		
		radioButton1.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		radioButton2.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		
		HBox box = new HBox();
		
		box.getChildren().addAll(topic, radioButton1, radioButton2);
		box.setTranslateX(-170);
		box.setTranslateY(90);
		
		return box;
	}

	private Pane radioButtonPane3() 
	{
		ToggleGroup tg = new ToggleGroup();
		
		Label topic = new Label(" Award Picture:                 ");
		
		radioButton1 = new RadioButton("True");
		radioButton2 = new RadioButton("False");
		
		radioButton1.setOnAction(actionHandler);
		radioButton2.setOnAction(actionHandler);
		
		radioButton1.setToggleGroup(tg);
		radioButton2.setToggleGroup(tg);
		
		radioButton1.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		radioButton2.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		
		HBox box = new HBox();
		
		box.getChildren().addAll(topic, radioButton1, radioButton2);
		box.setTranslateX(-170);
		box.setTranslateY(90);
		
		return box;
	}
	
	private Pane radioButtonPane4() 
	{
		ToggleGroup tg = new ToggleGroup();
		
		Label topic = new Label(" Award Directing:             ");
		
		radioButton1 = new RadioButton("True");
		radioButton2 = new RadioButton("False");
		
		radioButton1.setOnAction(actionHandler);
		radioButton2.setOnAction(actionHandler);
		
		radioButton1.setToggleGroup(tg);
		radioButton2.setToggleGroup(tg);
		
		radioButton1.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		radioButton2.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		
		HBox box = new HBox();
		
		box.getChildren().addAll(topic, radioButton1, radioButton2);
		box.setTranslateX(-170);
		box.setTranslateY(90);
		
		return box;
	}
	
	private Pane radioButtonPane5() 
	{
		ToggleGroup tg = new ToggleGroup();
			
		Label topic = new Label(" Award Cinematography: ");
			
		radioButton1 = new RadioButton("True");
		radioButton2 = new RadioButton("False");
			
		radioButton1.setOnAction(actionHandler);
		radioButton2.setOnAction(actionHandler);
			
		radioButton1.setToggleGroup(tg);
		radioButton2.setToggleGroup(tg);
			
		radioButton1.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		radioButton2.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
			
		HBox box = new HBox();
			
		box.getChildren().addAll(topic, radioButton1, radioButton2);
		box.setTranslateX(-170);	
		box.setTranslateY(90);
		
		return box;
	}
	
	private Pane radioButtonPane6() 
	{
		ToggleGroup tg = new ToggleGroup();
				
		Label topic = new Label(" Award Acting:	                 ");
				
		radioButton1 = new RadioButton("True");
		radioButton2 = new RadioButton("False");
				
		radioButton1.setOnAction(actionHandler);
		radioButton2.setOnAction(actionHandler);
				
		radioButton1.setToggleGroup(tg);
		radioButton2.setToggleGroup(tg);
				
		radioButton1.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		radioButton2.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
				
		HBox box = new HBox();
				
		box.getChildren().addAll(topic, radioButton1, radioButton2);
		box.setTranslateX(-170);
		box.setTranslateY(90);
		
		return box;
	}
	*/
	private Pane middlerightPane() 
	{
		FlowPane middlepane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		middlepane.setAlignment(Pos.TOP_LEFT);
		
		middlepane.getChildren().add(movieSlider());
		
		return middlepane;
	}
	
	/*
	 * [Level 2] Right Panel: Which holds the right side of the "Bottom Panel."  
	 */
	private Pane rightPane()
	{
		FlowPane rpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		rpane.setAlignment(Pos.TOP_LEFT);
		
		rpane.getChildren().add(toprightPane());
		rpane.getChildren().add(commentTextPane());
		
		rpane.setTranslateX(370);

		return rpane;
	}
	
	/*
	 * [Level 3] Top Area of Right Panel: Which will be the section that hold the "Summary Text" of the movie.
	 */
	private Pane toprightPane()
	{
		FlowPane topRpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		topRpane.setAlignment(Pos.TOP_RIGHT);
		
		topRpane.getChildren().add(ratedTextPane());
		topRpane.getChildren().add(yearTextPane());
		topRpane.getChildren().add(ratingTextPane());
		topRpane.getChildren().add(directorTextPane());
		topRpane.getChildren().add(summaryTextPane());
		topRpane.getChildren().add(genrePane());
		topRpane.getChildren().add(reviewerSpinner());
		
		topRpane.setTranslateY(20);
			
		return topRpane;
	}
	
	/*
	 * [Level 4]
	 */
	private Pane summaryTextPane()
	{
		FlowPane summaryPane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		summaryPane.setAlignment(Pos.TOP_LEFT);
		
		summaryPane.getChildren().add(createSummaryTextArea());
		
		summaryPane.setTranslateX(-1300);
		summaryPane.setTranslateY(60);
		
		return summaryPane;
	}
	
	/*
	 * [Level 5] Summary Text: 
	 */
	private Pane createSummaryTextArea()
	{
		textSummary = new TextArea("The Next Level, the gang is back but the game has changed. As they return\n"
				+ "to rescue one of their own, the players will have to brave parts unknown\n"
				+ "from a raid deserts to snowy mountains, to escape the world's most \n" + 
				"dangerous game.");
		//textArea = new TextArea();
		textSummary.setPrefRowCount(4);
		textSummary.setPrefColumnCount(40);
		
		textSummary.caretPositionProperty().addListener(this::changeCaret);
		
		return createTitledPane(textSummary, "Summary: ");
	}
	
	/*
	 * [Level 4] Genre Panel: 
	 */
	private Pane genrePane()
	{
		FlowPane gpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		gpane.setAlignment(Pos.TOP_LEFT);
		
		gpane.getChildren().add(checkBoxPane());
		
		gpane.setTranslateX(-1920);
		gpane.setTranslateY(220);
		
		return gpane;
	}
	
	/*
	 * [Level 5] Check Box Panel: 
	 */
	private Pane checkBoxPane()
	{
		checkBox1 = new CheckBox("Action");
		checkBox2 = new CheckBox("Adventure");
		checkBox3 = new CheckBox("Comedy");
		checkBox4 = new CheckBox("Drama");
		checkBox5 = new CheckBox("Fantasy");
		checkBox6 = new CheckBox("War");
		
		checkBox1.setOnAction(actionHandler);
		checkBox2.setOnAction(actionHandler);
		checkBox3.setOnAction(actionHandler);
		checkBox4.setOnAction(actionHandler);
		checkBox5.setOnAction(actionHandler);
		checkBox6.setOnAction(actionHandler);
		
		VBox box = new VBox();
		
		box.getChildren().add(checkBox1);
		box.getChildren().add(checkBox2);
		box.getChildren().add(checkBox3);
		box.getChildren().add(checkBox4);
		box.getChildren().add(checkBox5);
		box.getChildren().add(checkBox6);
		
		VBox.setMargin(checkBox1, new Insets(10.0, 0.0, 0.0, 0.0));
		
		return createTitledPane(box, "Genres: ");
	}
	
	/*
	 * [Level 3] 
	 */
	private Pane commentTextPane()
	{
		FlowPane trpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		trpane.setAlignment(Pos.BOTTOM_RIGHT);
			
		trpane.getChildren().add(createCommentTextArea());
		
		trpane.setTranslateX(-1825);
		trpane.setTranslateY(230);
			
		return trpane;
	}
	
	/*
	 * [Level 4]
	 */
	private Pane createCommentTextArea()
	{
		textArea = new TextArea();
		textArea.setPrefRowCount(10);
		textArea.setPrefColumnCount(16);
		
		textArea.caretPositionProperty().addListener(this::changeCaret);
		
		return createTitledPane(textArea, "Comments: ");
	}
	
	// (Change) Private Method: RIGHT Top Slider Pane
	private Pane movieSlider()
	{
		FlowPane sliderpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		sliderpane.setAlignment(Pos.TOP_RIGHT);
		
		sliderpane.getChildren().add(createSlider());
		
		sliderpane.setTranslateX(-1620);
		sliderpane.setTranslateY(240);
		
		return sliderpane;
	}
	
	// (Change) Private Method: RIGHT TOP Spinner Pane
	private Pane reviewerSpinner()
	{
		FlowPane spinnerpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		spinnerpane.setAlignment(Pos.TOP_RIGHT);
		
		spinnerpane.getChildren().add(createSpinner());
		
		spinnerpane.setTranslateX(-1745);
		spinnerpane.setTranslateY(-20);

		return spinnerpane;
	}

	private Pane directorTextPane()
	{
		FlowPane textpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		textpane.setAlignment(Pos.TOP_RIGHT);
		
		textpane.getChildren().add(createTextField());
		
		textpane.setTranslateX(-990);
		textpane.setTranslateY(220);
		
		return textpane;
	}
	
	private Pane ratingTextPane()
	{
		FlowPane textpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		textpane.setAlignment(Pos.TOP_RIGHT);
		
		textpane.getChildren().add(createTextRate());
		
		textpane.setTranslateX(-650);
		textpane.setTranslateY(220);
		
		return textpane;
	}
	
	private Pane yearTextPane()
	{
		FlowPane textpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		textpane.setAlignment(Pos.TOP_RIGHT);
		
		textpane.getChildren().add(createTextYear());
		
		textpane.setTranslateX(-674);
		textpane.setTranslateY(300);
		
		return textpane;
	}
	
	private Pane ratedTextPane()
	{
		FlowPane textpane = new FlowPane(Orientation.VERTICAL, 8.0, 8.0);
		textpane.setAlignment(Pos.TOP_RIGHT);
		
		textpane.getChildren().add(createTextRated());
		
		textpane.setTranslateX(-500);
		textpane.setTranslateY(10);
		
		return textpane;
	}
	//**********************************************************************
	// Private Methods (Widget Pane Creators)
	//**********************************************************************

	// Create a pane with a slider for the gallery. The progress bar and
	// slider show the same value from the model, so are synchronized.
	private Pane createSlider()
	{
		slider = new Slider(0.0, 230.0, 0.0);

		slider.setOrientation(Orientation.HORIZONTAL);
		slider.setMajorTickUnit(10.0);
		slider.setMinorTickCount(4);
		slider.setShowTickLabels(true);
		slider.setShowTickMarks(true);

		slider.valueProperty().addListener(this::changeDecimal);

		return createTitledPane(slider, "Duration: ");
	}

	// Create a pane with a spinner for the gallery. The progress bar,
	// slider, and spinner show the same value from the model, so stay synced.
	private Pane createSpinner()
	{
		spinner = new Spinner<Integer>(0, 100, 0, 1);

		spinner.setEditable(true);
		spinner.getEditor().setPrefColumnCount(4);

		spinner.valueProperty().addListener(this::changeInteger);

		return createTitledPane(spinner, "#'s of Reviews");
	}

	// Create a pane with a text field for the gallery.
	private Pane createTextField()
	{
		textField = new TextField();

		textField.setPrefColumnCount(11);

		textField.setOnAction(actionHandler);

		return createTitledPane(textField, "Director: ");
	}
	
	// Create a pane with a text field for the gallery.
	private Pane createTextRate()
	{
		textAge = new TextField("PG-13");

		textAge.setPrefColumnCount(6);

		textAge.setOnAction(actionHandler);

		return createTitledPane(textAge, "Rating Age: ");
	}
	
	private Pane createTextYear()
	{
		textYear = new TextField("2019");

		textYear.setPrefColumnCount(11);

		textYear.setOnAction(actionHandler);

		return createTitledPane(textYear, "Release Year: ");
	}

	private Pane createTextRated()
	{
		Label topic = new Label("Rated: ");
		Label rate = new Label(" out of 10.");
		
		textRating = new TextField("7.5");

		textRating.setPrefColumnCount(6);

		textRating.setOnAction(actionHandler);
		
		textRating.setPadding(new Insets(0.0, 4.0, 0.0, 4.0));
		
		HBox box = new HBox();
		
		box.getChildren().addAll(topic, textRating, rate);

		return box;
	}


	//**********************************************************************
	// Private Methods (Property Change Handlers)
	//**********************************************************************

	private void changeDecimal(ObservableValue<? extends Number> observable,
								  Number oldValue, Number newValue)
	{
		if (observable == slider.valueProperty())
			controller.set("myDouble", newValue);
	}

	private void changeInteger(ObservableValue<? extends Number> observable,
								  Number oldValue, Number newValue)
	{
		if (observable == spinner.valueProperty())
			controller.set("myInt", newValue);
	}

	private void changeComment(ObservableValue<? extends String> observable,
			  String oldValue, String newValue)
	{
		if (observable == textArea.textProperty())
			controller.set("comment", newValue);
		if(observable == textSummary.textProperty())
			controller.set("summary", newValue);
	}
	
	private void changeCaret(ObservableValue<? extends Number> observable,
			Number oldValue, Number newValue)
	{
		if (ignoreCaretEvents)
			return;

		if (observable == textArea.caretPositionProperty())
			controller.set("comment", textArea.getText());
		if (observable == textSummary.caretPositionProperty())
			controller.set("summary", textSummary.getText());
	}
	
	//**********************************************************************
	// Inner Classes (Event Handlers)
	//**********************************************************************

	private final class ActionHandler
		implements EventHandler<ActionEvent>
	{
		public void	handle(ActionEvent e)
		{
			Object	source = e.getSource();

			if (source == textField)
				controller.set("myString", textField.getText());
			else if (source == textRating)
				controller.set("myRating", textRating.getText());
			else if (source == textYear)
				controller.set("myYear", textYear.getText());
			else if (source == textAge)
				controller.set("myAge", textAge.getText());
			else if (e.getSource() == checkBox1)
				controller.set("Action", checkBox1.isSelected());
			else if (e.getSource() == checkBox2)
				controller.set("Adventure", checkBox2.isSelected());
			else if (e.getSource() == checkBox3)
				controller.set("Comedy", checkBox3.isSelected());
			else if (e.getSource() == checkBox4)
				controller.set("Drama", checkBox4.isSelected());
			else if (e.getSource() == checkBox5)
				controller.set("Fantasy", checkBox5.isSelected());
			else if (e.getSource() == checkBox6)
				controller.set("War", checkBox6.isSelected());
			else if (e.getSource() == checkBox7)
				controller.set("Is Animated:", checkBox7.isSelected());
			else if (e.getSource() == checkBox8)
				controller.set("Is Color:", checkBox8.isSelected());
			else if (e.getSource() == checkBox9)
				controller.set("Award Picture:", checkBox9.isSelected());
			else if (e.getSource() == checkBox10)
				controller.set("Award Directing:", checkBox10.isSelected());
			else if (e.getSource() == checkBox11)
				controller.set("Award Cinematography:", checkBox11.isSelected());
			else if (e.getSource() == checkBox12)
				controller.set("Award Acting:", checkBox12.isSelected());
			
			//else if (e.getSource() == radioButton1)
				//controller.set("choice", "True");
			//else if (e.getSource() == radioButton2)
				//controller.set("choice", "False");
		}
	}
}

package edu.ou.cs.hci.assignment.prototypea.pane;

//import java.lang.*;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

import edu.ou.cs.hci.assignment.prototypea.Controller;
import edu.ou.cs.hci.resources.Resources;
import javafx.scene.Node;
import javafx.scene.Parent;
import javafx.scene.control.Tab;
import javafx.scene.control.TitledPane;
import javafx.scene.control.Tooltip;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.scene.layout.Background;
import javafx.scene.layout.BackgroundFill;
import javafx.scene.layout.Pane;
import javafx.scene.layout.Region;
import javafx.scene.layout.StackPane;
import javafx.scene.paint.Color;

//******************************************************************************

/**
 * The <CODE>AbstractPane</CODE> class.
 *
 * @author  Chris Weaver
 * @version %I%, %G%
 */
public abstract class AbstractPane
{
	//**********************************************************************
	// Public Class Members
	//**********************************************************************

	public static final String	RSRC		= "edu/ou/cs/hci/resources/";

	public static final String	SWING_ICON	= RSRC + "example/swing/icon/";
	public static final String	FX_ICON	= RSRC + "example/fx/icon/";

	public static final String	FX_TEXT	= "example/fx/text/";

	//**********************************************************************
	// Private Members
	//**********************************************************************

	// Master of the program, manager of the data, mediator of all updates
	protected final Controller	controller;
	protected final String		name;
	protected final String		hint;

	// Provided when the subclass constructor calls setBase()
	protected Node				base;

	//**********************************************************************
	// Constructors and Finalizer
	//**********************************************************************

	protected AbstractPane(Controller controller, String name, String hint)
	{
		this.controller = controller;
		this.name = name;
		this.hint = hint;
	}

	//**********************************************************************
	// Getters and Setters
	//**********************************************************************

	public String	getName()
	{
		return name;
	}

	public String	getHint()
	{
		return hint;
	}

	public Node	getBase()
	{
		return base;
	}

	// Called by the subclass constructor to provide its scene subgraph.
	protected void	setBase(Node base)
	{
		this.base = base;
	}

	//**********************************************************************
	// Public Methods
	//**********************************************************************

	// Convenience method to put the base node into a tab. Warning: Don't
	// attempt to layout both the base node and tabs containing it! (Each
	// node can be included only once in a scene graph.)
	public Tab	createTab()
	{
		return createFixedTab(base, name, hint);
	}

	//**********************************************************************
	// Public Methods (Controller)
	//**********************************************************************

	// The controller calls this method when it adds a view.
	// Set up the nodes in the view with data accessed through the controller.
	public void	initialize()
	{
	}

	// The controller calls this method when it removes a view.
	// Unregister event and property listeners for the nodes in the view.
	public void	terminate()
	{
	}

	// The controller calls this method whenever something changes in the model.
	// Update the nodes in the view to reflect the change.
	public void	update(String key, Object value)
	{
	}

	//**********************************************************************
	// Public Class Methods (Resources)
	//**********************************************************************

	// Convenience method to create a node for an image located in resources
	// relative to the SWING_ICON package. See static member definitions above.
	public static ImageView	createSwingIcon(String url, int size)
	{
		Image	image = new Image(SWING_ICON + url, size, size, false, false);

		return new ImageView(image);
	}

	// Convenience method to create a node for an image located in resources
	// relative to the FX_ICON package. See static member definitions above.
	public static ImageView	createFXIcon(String url, double w, double h)
	{
		Image	image = new Image(FX_ICON + url, w, h, false, true);

		return new ImageView(image);
	}

	public static List<List<String>>	loadFXData(String url)
	{
		ArrayList<String>	lines = Resources.getLines(FX_TEXT + url);
		List<List<String>>	data = new ArrayList<List<String>>();

		for (String item : lines)
		{
			StringTokenizer	st = new StringTokenizer(item, ",");
			ArrayList<String>	record = new ArrayList<String>();

			while (st.hasMoreTokens())
				record.add(st.nextToken());

			data.add(record);
		}

		return data;
	}

	//**********************************************************************
	// Public Class Methods (Layout)
	//**********************************************************************

	// Convenience method to create an unclosable tab with a tooltip.
	public static Tab	createFixedTab(Node node, String title, String text)
	{
		Tab	tab = new Tab(title, node);

		tab.setClosable(false);
		tab.setTooltip(new Tooltip(text));

		return tab;
	}

	// Convenience method to lookup nodes inside others in the scene graph.
	public static Node	getDescendant(Node node, int... index)
	{
		for (int i=0; i<index.length; i++)
		{
			if (!(node instanceof Parent))
				throw new IllegalArgumentException("Ancestor is not a Parent");

			node = ((Parent)node).getChildrenUnmodifiable().get(index[i]);
		}

		return node;
	}

	// JavaFX doesn't have a Swing-style TitledBorder, so use a TitledPane.
	// TitledPanes usually go in Accordians, but can be used independently.
	public static Pane	createTitledPane(Region region, String title)
	{
		StackPane	stackPane = new StackPane(region);

		stackPane.setId("gallery-pane");

		TitledPane	titledPane = new TitledPane(title, stackPane);

		titledPane.setCollapsible(false);	// Usually true, in Accordians

		return new StackPane(titledPane);
	}

	// This is the procedural version. The declarative CSS version would look
	// like, e.g. region.setStyle("-fs-background-color: white;")
	public static void	setBackgroundColor(Region region, Color color)
	{
		BackgroundFill	bf = new BackgroundFill(color, null, null);
		Background		bg = new Background(bf);

		region.setBackground(bg);
	}
}
