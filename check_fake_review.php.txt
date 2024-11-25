document.getElementById('review-form').addEventListener('submit', function(event) {
    event.preventDefault();
    
    const reviewText = document.getElementById('review-input').value;
    
    if (reviewText.trim() === "") {
        alert("Please enter a review.");
        return;
    }

    // Send the review to the PHP backend for processing
    fetch('check_fake_review.php', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify({ review: reviewText })
    })
    .then(response => response.json())
    .then(data => {
        // Display the result of the review check
        document.getElementById('result').innerHTML = `Result: ${data.status} <br> ${data.message}`;
    })
    .catch(error => {
        document.getElementById('result').innerHTML = 'An error occurred. Please try again later.';
    });
});
